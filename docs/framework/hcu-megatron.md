# hcu-megatron on HCU

> 本文档涵盖 hcu-megatron 在 HCU 环境下的安装、配置及各特性的使用说明。

- [简介](#简介)
- [安装](#安装)
  - [方式一：pip 安装 whl 包](#方式一pip-安装-whl-包)
  - [方式二：源码下载与编译](#方式二源码下载与编译)
- [使用方式](#使用方式)
  - [集成到 Megatron-LM](#集成到-megatron-lm)
  - [运行训练](#运行训练)
- [特性说明](#特性说明)
  - [流水线并行](#流水线并行)
  - [RiPipe 重计算独立调度](#ripipe-重计算独立调度)
  - [Seq1F1B 长序列流水线](#seq1f1b-长序列流水线)
  - [张量并行 Flux 加速](#张量并行-flux-加速)
  - [all2all 量化通信](#all2all-量化通信)
  - [参数副本复用](#参数副本复用)
  - [激活函数重计算](#激活函数重计算)
  - [异步激活值 Offload](#异步激活值-offload)
  - [指定重计算层](#指定重计算层)
  - [内存缓存 Checkpoint](#内存缓存-checkpoint)
  - [EDGC 动态梯度压缩](#edgc-动态梯度压缩)
  - [MHC 超连接](#mhc-超连接)
  - [Megatron-Bridge](#megatron-bridge)

## 简介

hcu-megatron 是面向 HCU 环境的 Megatron-LM 增强库，通过替换 Megatron 的函数或类，引入新特性或实现更好的训练性能。核心能力包括：

- **流水线并行优化**：支持 interleaved 1f1b MoE A2A overlap、DualPipeV、ZB-H1、RiPipe 等多种高效流水线调度策略
- **显存优化**：支持激活函数重计算、异步激活值 offload、参数副本复用、指定层重计算等多种显存节省手段
- **通信优化**：支持基于 Flux 的 TP 计算通信 overlap、all2all 量化通信（int4/int8）、EDGC 动态梯度压缩
- **长序列训练**：支持 Seq1F1B 序列级流水线调度，可在不使用重计算的情况下训练 64k 长序列
- **模型扩展**：通过 Megatron-Bridge 支持更多 HuggingFace 模型架构直接接入 Megatron 训练
- **MHC**：支持 Hyper Connections（多残差流）特性，提供 torch 原生和 tile_kernel 两种实现

源码仓库: https://developer.sourcefind.cn/codes/OpenDAS/dcu_megatron/-/tree/core_v0.17.0/ 

## 安装

> 版本依赖：dtk >= 25.04，transformer-engine >= 2.4.0，torch >= 2.6.0

### 方式一：pip 安装 whl 包

直接下载已编译好的 whl 包安装：

```bash
pip install hcu_megatron*.whl
```

### 方式二：源码下载与编译

**1. 下载源码**

git 方式：

```bash
git clone -b core_v0.17.0 --recurse-submodules http://112.11.119.99:10068/hcutoolkit/deeplearing/hcu_megatron.git
```

离线方式：

1. 下载仓库离线代码包
2. 点击 `Megatron-LM@版本号`，下载对应版本的 Megatron-LM 离线代码包
3. 将 Megatron-LM 离线代码包解压到 `hcu_megatron/Megatron-LM` 目录下

**2. 编译并安装**

```bash
cd hcu_megatron
python3 setup.py -v bdist_wheel
pip install dist/hcu_megatron*.whl
```

## 使用方式

### 集成到 Megatron-LM

在 Megatron-LM 目录下的 `pretrain_gpt.py` 中新增一行导入：

```python
from megatron.training.arguments import core_transformer_config_from_args
from megatron.training.yaml_arguments import core_transformer_config_from_yaml
from megatron.core.models.gpt.gpt_layer_specs import (
    get_gpt_decoder_block_spec,
    get_gpt_layer_local_spec,
    get_gpt_layer_with_transformer_engine_spec,
    get_gpt_mtp_block_spec,
)

from hcu_megatron import megatron_adaptor     # 新增此行
```

使用时需确保 hcu-megatron 版本与 Megatron-LM 版本对应。

### 运行训练

进入 `examples` 目录，选择对应模型的执行脚本：

```
examples/
├── deepseek_v3
├── gpt3
├── llama
├── mixtral
└── qwen
```

以 DeepSeek V3 671B 为例：

```bash
cd examples/deepseek_v3
# num_nodes 为运行的节点数 默认8卡/机
bash run_deepseekv3_671B.sh hostfile_deepseekv3_671B num_nodes
```

## 特性说明

### 流水线并行

#### interleaved 1f1b MoE A2A overlap

针对 MoE 模型，EP 间的 A2A 通信在端到端时间中占据较大比重。hcu-megatron 支持基于 interleaved 1f1b 的 MoE A2A 通信与计算 overlap：

```bash
--overlap-moe-expert-parallel-comm
```

若前向计算无法完全掩盖 EP 通信，可拆分反向 dw 计算：

```bash
--delay-wgrad-compute
```

开启 `--delay-wgrad-compute` 同时开启 `--overlap-grad-reduce` 时，需额外设置：

```bash
export NVTE_OVERLAP_GRAD_REDUCE=1
```

#### DualPipeV 流水线

每个 stage 上有两个模型 chunk，支持 MoE A2A overlap：

```bash
--schedule-method dualpipev
--delay-wgrad-compute          # dualpipev 自动开启，可省略

# 开启 MoE A2A overlap
--overlap-moe-expert-parallel-comm
--overlap-ep-comm-with-split-attn  # 可选，将 attn 拆分为三部分

# 自定义每个 chunk 的 transformer 层数（整数或数组）
--num-layers-to-build  ***
```

#### ZB-H1 流水线

通过拆分参数/激活值梯度计算减少流水线气泡，在小 batch 场景下训练性能有明显提升：

```bash
--schedule-method zb_h1
--delay-wgrad-compute          # zb_h1 自动开启，可省略
```

> 注意：需满足流水线 stage 数大于 1；不支持开启 vp。

#### 1f1b cooldown 阶段优化

对 1f1b 流水线 cooldown 阶段的参数/激活值梯度计算进行拆分，提升小 batch 场景训练性能：

```bash
--delay-1f1b-cooldown-wgrad-compute
--delay-wgrad-compute          # 使用上述参数时自动开启，可省略
```

> 注意：需满足流水线 stage 数大于 1；不支持开启 vp。

---

### RiPipe 重计算独立调度

RiPipe（Recompute independent Pipelining）将重计算从反向计算中解耦，由调度器主动触发，提供两种模式：

- **recompute-in-advance**：提前重计算，减少流水线气泡，提升性能
- **recompute-in-bubble**：利用流水线气泡时间执行重计算，以极小性能开销节省显存

#### recompute-in-advance 配置

```bash
--schedule-method=ripipe
--recompute-in-advance
--recompute-num-layers 1

# 必需的流水线配置
--pipeline-model-parallel-size 8
--virtual-pipeline-model-parallel-size 8
--num-layers-per-virtual-pipeline-stage 1

# 必需的重计算配置
--recompute-granularity full
--recompute-method block
--recompute-modules mlp
```

#### recompute-in-bubble 配置

```bash
--schedule-method=ripipe
--recompute-in-bubble

# 必需的流水线配置
--pipeline-model-parallel-size 8
--virtual-pipeline-model-parallel-size 8
--num-layers-per-virtual-pipeline-stage 1
# 不开启重计算
```

> 兼容性限制：两种模式均不兼容完全重计算 uniform/block、选择重计算、自适应选择重计算、`no-align-grad-reduce`、`no-overlap-p2p-communication`；两者不可同时开启。

---

### Seq1F1B 长序列流水线

Seq1F1B 将批次级别的调度单元分解为序列级别，减少显存占用和流水线气泡，支持在 64 个 A100 GPU 上训练 300 亿参数模型、序列长度达 64k（无需重计算）。

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `--pipe-sp-strategy` | str | `uniform_comp` | 序列切割方式：`uniform_comp`（按计算量均衡切割）或 `average`（均匀切割） |
| `--pipe-sp-splits` | int | `1` | seq 切分段数，由显存决定，尽量减小切分段数 |
| `--use-flash-attn` | bool | `true` | 使用 seq1f1b 时必须开启 |
| `--schedule-method` | str | `seq1f1b` | 使用 seq1f1b 时必须设置，还支持 `interleaved_seg1f1b` |

> 注意：暂不支持激活值重计算；不支持 transformer engine；仅支持 mcore + local 或 legacy + local 方式；推荐 `uniform_comp + seq1f1b` 组合。

---

### 张量并行 Flux 加速

基于 [Flux](https://github.com/bytedance/flux) 的 TP 计算通信融合，通过计算掩盖 GPU 间通信，提升训练/推理性能：

```bash
--parallel-linear-impl flux
```

保存前向 all-gather 数据用于反向权重梯度计算，避免反向再次 all-gather：

```bash
--save-flux-gather-input
```

不使用 flux kernel 融合反向部分计算通信：

```bash
--disable-bw-flux-gemmrs-op
```

---

### all2all 量化通信

对 all2all 通信数据进行低精度量化，减少通信量。支持将 bf16 数据量化为 int8 或 int4 后再通信：

**必需参数：**

```bash
--use-quantize-comm
```

**可选参数：**

```bash
--quant-comm-bits 4       # 量化精度：4（int4）或 8（int8），默认 8
--quant-group-size 32     # 分组大小：quant-comm-bits=4 时可取 16/32（默认 32）；
                          # quant-comm-bits=8 时可取 64/128（默认 128）
```

---

### 参数副本复用

在 BF16 训练场景中，通过将 FP32 参数转换为 BF16 + 残差的方式复用内存，节省一份 BF16 参数的显存：

```bash
--use-optimizer-feature
--reuse-fp32-param
```

---

### 激活函数重计算

针对 gelu 等激活函数输出数据量大但计算量小的特点，通过灵活插入重计算节省激活函数输出的显存，性能损失极小：

```bash
# 必选
--recompute-activation-function

# 可选，指定激活函数重计算的层数
--recompute-activation-function-num-layers ${num}
```

**与全重计算同时开启说明：**

- 仅支持 `--recompute-method block`
- 全重计算层与激活函数重计算层互斥，不会重叠
- 未开启流水线并行时，两者层数之和应等于总层数
- 暂不兼容自适应重计算

| 模型 | 参数配置 | 设备数 | 显存收益 | 性能下降 |
|------|---------|--------|---------|---------|
| llama2-7B | seq-length 4096，TP 1，PP 2 | 8卡（单机） | 2.6G（4%） | 约 2% |

---

### 异步激活值 Offload

前向计算时将激活值异步拷贝到 CPU，反向计算前再异步拷贝回 HCU，以更小的性能损失达到与重计算相同的显存降低效果：

```bash
# 必选
--swap-attention

# 可选，控制 offload 的模块（默认 self_attention，建议只开启此项）
--swap-modules input_layernorm,self_attention,post_attention_norm

# 可选，控制 offload 的层
--specify-layers 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15
```

> 注意：mcore 模式下需设置 `overlap_grad_reduce=True`，且 te >= 2.5。

---

### 指定重计算层

支持对指定 transformer/mtp 层进行重计算，在显存满足要求的同时提高训练性能：

```bash
--recompute-granularity full
--recompute-layer-ids 0 4 8 12      # 对第 0、4、8、12 transformer 层重计算（从 0 编号）
--recompute-mtp-layer-ids 0         # 对第 0 mtp 层重计算（从 0 编号）
```

> 注意：`recompute-layer-ids` 范围为 `[0, N_total_layers-1]`；`recompute-mtp-layer-ids` 范围为 `[0, N_total_mtp_layers-1]`；两者可同时设置或只设置一个；不允许设置 `--recompute-method` 参数。

---

### 内存缓存 Checkpoint

在大模型训练中使用内存缓存 ckpt 提升保存性能：

```bash
--use-ckpt-memory-cache
```

**依赖：**

1. 安装 hyckpt 包：`pip install hyckpt-1.0.1-py3-none-any.whl`
2. 启动 hyckptd 进程：
   ```bash
   mpirun -pernode -hostfile <主机名文件> hyckptd --log <日志文件路径>
   ```

---

### EDGC 动态梯度压缩

EDGC（Entropy-driven Dynamic Gradient Compression）通过低秩分解与误差反馈机制，动态调整梯度压缩率，在显著降低通信开销的同时保障收敛精度。

**启用方式（仅需此一个参数，其余参数默认值已调优）：**

```bash
--enable-dynamic-grad-comp
```

**核心参数：**

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--grad-comp-warm-up` | `0.1` | 压缩预热比例，前 X% 步不启用压缩 |
| `--rank-adjust-window-size` | `1000` | 动态秩调节的观测窗口大小（迭代次数） |
| `--iteration-sample-ratio` | `0.1` | 性能采样比例，降低探测开销 |
| `--gradient-sample-ratio` | `0.1` | 梯度采样比例，加快决策速度 |
| `--collect-log-path` | `./logs` | EDGC 系统日志输出路径 |

**适用场景：** 参数量 > 1B 的 LLM 训练、高延迟/低带宽网络、计算-通信失衡系统、长周期训练任务。

**常见问题：**

- 收敛变慢：提高 `--grad-comp-warm-up`（如改为 `0.2`）或关闭 `--enable-dynamic-grad-comp`
- OOM：将 `compression_dtype` 和 `ef_store_dtype` 设为 `bf16`
- 通信时间未下降：EDGC 更适用于 > 1B 参数模型，检查压缩是否在 AllReduce 前正确执行

---

### MHC 超连接

hcu-megatron 0.17.0 新增 MHC（Hyper Connections）实现，提供 torch 原生和 tile_kernel 两种方式：

**torch 原生实现（支持重计算）：**

```bash
--enable-hyper-connections
```

**tile_kernel 实现（不支持重计算）：**

```bash
--enable-hyper-connections
--mhc-use-tilekernels
--mhc-fuse-h-post-compute
--mhc-tau 1.0
--mhc-log-amax-per-step 20
```

使用 tile_kernel 前需完成以下配置：

```bash
# 设置 tile_kernels 路径（假设在 Megatron-LM/megatron 目录下）
export PYTHONPATH=/mnt/hcu_megatron/Megatron-LM/megatron/:$PYTHONPATH

# 设置 z3/lib 路径
export LD_LIBRARY_PATH="/usr/local/lib/python3.11/site-packages/z3/lib:$LD_LIBRARY_PATH"
```

**开启 MHC 重计算（仅 torch 原生实现支持）：**

```bash
--recompute-granularity selective
--recompute-modules layernorm core_attn mhc
```

> 注意：`--mhc-sinkhorn-iterations` 参数需设置为 ≤ 10。

---

### Megatron-Bridge

基于 Megatron-Bridge 可通过 Megatron 训练更多 HuggingFace 模型架构，无需手动转换模型配置：

```bash
--use-bridge
--bridge-hf-model ${TOKENIZER_MODEL_PATH}
--load-weights   # 可选，加载 HF 预训练权重
```

Bridge 通过读取 HF `config.json` 中的 `architectures` 字段自动分发到对应的 Bridge 实现，将 HF 模型配置转换为 Megatron 格式并构建分布式模型。
