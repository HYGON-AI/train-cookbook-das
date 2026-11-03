# 重计算优化

hcu-megatron 在 Megatron-LM 原有重计算能力之外，提供了 RiPipe 重计算独立调度、激活函数重计算和指定层重计算三种更精细的重计算策略，用于在显存与性能之间做更好的权衡。

- [RiPipe 重计算独立调度](#ripipe-重计算独立调度)
- [激活函数重计算](#激活函数重计算)
- [指定重计算层](#指定重计算层)

## RiPipe 重计算独立调度

原生流水线中重计算由反向计算触发，与反向计算绑定调度；但重计算并不依赖反向梯度，这会导致气泡增多和性能下降。RiPipe（Recompute independent Pipelining）将重计算从反向计算中解耦，由调度器主动触发，提供两种模式：

- **recompute-in-advance**：提前重计算，减少流水线气泡，提升性能
- **recompute-in-bubble**：利用流水线气泡时间执行重计算，以极小性能开销节省显存

### recompute-in-advance 配置

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

### recompute-in-bubble 配置

```bash
--schedule-method=ripipe
--recompute-in-bubble

# 必需的流水线配置
--pipeline-model-parallel-size 8
--virtual-pipeline-model-parallel-size 8
--num-layers-per-virtual-pipeline-stage 1
# 不开启重计算
```

### 兼容性限制

- `--recompute-in-bubble` 不兼容完全重计算 uniform/block、选择重计算、自适应选择重计算、`swap-attention`、`no-align-grad-reduce`、`no-overlap-p2p-communication`
- `--recompute-in-bubble` 不兼容 MoE 场景下的 `--moe-adaptive-recompute-activation`、`--moe-layer-recompute`
- `--recompute-in-advance` 不兼容完全重计算 uniform/block、选择重计算、自适应选择重计算、`no-align-grad-reduce`、`no-overlap-p2p-communication`
- `--recompute-in-bubble` 与 `--recompute-in-advance` 不可同时开启

## 激活函数重计算

针对 gelu 等激活函数「输出数据量大但计算量小」的特点，通过灵活插入重计算节省激活函数输出的显存，性能损失极小：

```bash
# 必选
--recompute-activation-function

# 可选，指定激活函数重计算的层数
--recompute-activation-function-num-layers ${num}
```

### 与全重计算同时开启说明

- 仅支持 `--recompute-method block`
- 全重计算层与激活函数重计算层互斥，不会有一层既做全重计算又做激活函数重计算
- 执行优先级：先做全重计算层，后做激活函数重计算层
- 未开启流水线并行时，全重计算层数和激活函数重计算层数之和应等于总层数
- 暂不兼容自适应重计算特性

### 使用效果

| 模型 | 参数配置 | 设备数 | 显存收益 | 性能下降 |
|------|---------|--------|---------|---------|
| llama2-7B | seq-length 4096，TP 1，PP 2 | 8 卡（单机） | 2.6G（4%） | 约 2% |

## 指定重计算层

Megatron 原生支持对所有 transformer/mtp 层进行重计算，显存占用小但性能通常较差。hcu-megatron 支持对指定层进行重计算，在显存满足要求的同时提高训练性能：

```bash
--recompute-granularity full
--recompute-layer-ids 0 4 8 12       # 对第 0、4、8、12 transformer 层重计算（从 0 编号）
--recompute-mtp-layer-ids 0          # 对第 0 mtp 层重计算（从 0 编号）
```

### 注意事项

1. `--recompute-layer-ids` 取值范围为 `[0, N_total_layers-1]`，`N_total_layers` 为模型总 transformer 层数
2. `--recompute-mtp-layer-ids` 取值范围为 `[0, N_total_mtp_layers-1]`，`N_total_mtp_layers` 为模型总 mtp 层数
3. 两者允许同时设置或只设置一个；未设置时相应网络层不做重计算
4. 不允许设置 `--recompute-method` 参数
