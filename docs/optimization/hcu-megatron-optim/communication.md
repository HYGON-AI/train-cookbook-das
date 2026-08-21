# 通信优化

hcu-megatron 针对训练中的通信瓶颈，提供张量并行 Flux 加速、all2all 量化通信和 EDGC 动态梯度压缩三种优化手段，覆盖 TP 计算通信 overlap、MoE 场景通信量压缩、跨节点梯度同步压缩等常见场景。

- [张量并行 Flux 加速](#张量并行-flux-加速)
- [all2all 量化通信](#all2all-量化通信)
- [EDGC 动态梯度压缩](#edgc-动态梯度压缩)

## 张量并行 Flux 加速

基于 [Flux](https://github.com/bytedance/flux)（字节提供的通算融合库）的 TP 计算通信融合，通过计算掩盖 GPU 间的通信，提升训练/推理性能。使用 Flux 相关 kernel 融合 TP 中的计算与通信：

```bash
--parallel-linear-impl flux
```

### 保存前向 AG 结果用于反向

保存前向 all-gather 数据用于反向权重梯度计算，避免反向再次 all-gather：

```bash
--save-flux-gather-input
```

### 不使用 flux kernel 融合反向部分

对反向部分的计算通信，可以不使用 flux kernel 融合。此时反向 RS 与 QKW_WGRAD/FC1_WGRAD 进行 overlap；若不使用 `--save-flux-gather-input`，则 QKV_DGRAD/FC1_DGRAD 与 AG 进行 overlap：

```bash
--disable-bw-flux-gemmrs-op
```

## all2all 量化通信

对 all2all 通信数据进行低精度量化，减少通信量。默认 all2all 数据类型为 bf16，本项目支持将数据量化为 int8 或 int4 后再进行 all2all 通信。

**必需参数：**

```bash
--use-quantize-comm
```

**可选参数：**

```bash
--quant-comm-bits 4       # 量化精度：4（int4）或 8（int8），默认 8
--quant-group-size 32     # 分组大小：
                          #   quant-comm-bits=4 时可取 16/32（默认 32）
                          #   quant-comm-bits=8 时可取 64/128（默认 128）
                          # 数据被分成 quant-group-size 大小的组，每组应用特定量化策略，
                          # 有助于提高量化效果或保持模型性能
```

## EDGC 动态梯度压缩

EDGC（Entropy-driven Dynamic Gradient Compression）是面向大规模 LLM 分布式训练的高效动态梯度压缩框架，通过「低秩分解 + 误差反馈」的思路，根据训练阶段、系统环境及流水线各层的梯度熵变化，动态调整梯度压缩率，在显著降低通信开销的同时保留关键梯度信息，兼顾训练效率与模型收敛精度。

### 核心设计

- **动态压缩调度**：训练初期禁用压缩（预热），进入稳定期后逐步启用并动态调整压缩率
- **差异化压缩**：利用非瓶颈 stage 的时间冗余窗口提高压缩强度，关键路径 stage 保留低压缩比
- **误差反馈（Error Feedback）**：持久化存储压缩残差，保障长期训练的收敛稳定性

### 启用方式

只需添加此一个参数即可启用 EDGC，其余参数默认值已在多种典型场景中验证为最优，一般无需修改：

```bash
--enable-dynamic-grad-comp
```

### 核心参数

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `--enable-dynamic-grad-comp` | bool | `False` | 是否启用 EDGC 框架 |
| `--grad-comp-warm-up` | float32 | `0.1` | 压缩预热比例。前 X% 步不启用压缩，避免初期梯度剧烈变化时压缩带来的方向偏移 |
| `--rank-adjust-window-size` | int | `1000` | 动态秩调节的观测窗口大小（迭代次数）。窗口越大越稳定，越小响应越快 |
| `--iteration-sample-ratio` | float32 | `0.1` | 性能采样比例。每个调节窗口内仅对该比例的迭代做性能探测，降低开销 |
| `--gradient-sample-ratio` | float32 | `0.1` | 梯度采样比例。性能探针阶段仅对部分梯度做低秩分解测试 |
| `--collect-log-path` | str | `./logs` | EDGC 系统日志输出路径，用于保存压缩率、秩变化、通信时间等监控信息 |
| `compression_dtype` | str | `bf16` | 压缩过程中间变量的数据类型（低秩矩阵 P/Q 的计算精度），推荐 `bf16` |
| `ef_store_dtype` | str | `bf16` | 误差反馈缓冲区的存储精度，推荐 `bf16` 以节省显存 |
| `use_error-feedback` | bool | `True` | 是否启用误差反馈机制，强烈建议保持开启 |
| `rank_adjust_step` | int | `4` | 每次调整压缩秩的最大步长，防止压缩强度突变 |

### 适用场景

- **大规模 LLM 训练**：参数量 > 1B，梯度通信成为主要瓶颈
- **高延迟/低带宽网络**：跨数据中心、云边协同、RoCE 受限
- **计算-通信失衡系统**：高端 GPU 搭配中等网络（如 25Gbps），GPU 算力过剩通信拖累
- **长周期训练任务**：训练持续数天甚至数周

### 不适用场景

| 场景 | 原因 |
|------|------|
| 极短训练周期（< 1 小时） | 压缩收益不足以覆盖初始化开销 |
| 模型极小（< 10M 参数） | 通信开销本身很低，压缩反而引入额外计算负担 |
| 对收敛精度要求极高 | 虽然 EF 机制已极大缓解失真，但仍属有损压缩 |
| 使用极稀疏梯度算法 | 可能与现有稀疏化策略冲突 |

### 常见问题

**1. 压缩后模型收敛变慢或不收敛**
- 原因：压缩过强（秩太低）
- 解决：提高 `--grad-comp-warm-up`（如从 `0.1` 改为 `0.2`）；或关闭 `--enable-dynamic-grad-comp`

**2. 显存爆了（OOM）**
- 原因：EDGC 需存储误差缓冲区，带来 2%~6% 额外显存占用
- 解决：将 `compression_dtype` 和 `ef_store_dtype` 设为 `bf16`；若使用 ZeRO，开启分片模式

**3. 通信时间未下降**
- 原因：模型太小或 batch size 太小，通信本就不成瓶颈；或压缩逻辑未正确集成
- 解决：EDGC 更适用于 > 1B 参数模型；检查压缩是否在 `AllReduce` 前正确执行

**4. 初始训练阶段 `edgc_utils` 报错**
- 原因：通信未成为瓶颈，或压缩成本高于通信时间
- 解决：关闭 EDGC：`--enable-dynamic-grad-comp=False`
