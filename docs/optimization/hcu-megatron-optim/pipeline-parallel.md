# 流水线并行优化

hcu-megatron 在 Megatron-LM 已有流水线调度基础上进行了优化，并提供多种额外的流水线方法，覆盖 MoE 通算 overlap、DualPipeV、ZB-H1、1f1b cooldown 拆分、长序列 Seq1F1B 等场景。

- [interleaved 1f1b MoE A2A overlap](#interleaved-1f1b-moe-a2a-overlap)
- [DualPipeV 流水线](#dualpipev-流水线)
- [ZB-H1 流水线](#zb-h1-流水线)
- [1f1b cooldown 阶段优化](#1f1b-cooldown-阶段优化)
- [Seq1F1B 长序列流水线](#seq1f1b-长序列流水线)

## interleaved 1f1b MoE A2A overlap

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

若同时开启 TP 与 EP，可通过将 attn 拆分为 qkv/core_attn/proj 三部分缓解 tp 与 ep 竞争（hcu-megatron 默认使用此调度）：

```bash
--overlap-ep-comm-with-split-attn
```

## DualPipeV 流水线

每个 stage 上有两个模型 chunk，两个 micro batch 的 forward/backward 之间的 EP A2A 通信可与计算 overlap，支持 MoE A2A overlap：

```bash
--schedule-method dualpipev
--delay-wgrad-compute              # dualpipev 自动开启，可省略

# 开启 MoE A2A overlap
--overlap-moe-expert-parallel-comm
--overlap-ep-comm-with-split-attn  # 可选，将 attn 拆分为三部分

# 自定义每个 chunk 的 transformer 层数（整数或数组）
# 整数：每个 chunk 上的网络层数；
# 数组：长度为 stage 数的两倍，元素值为对应 chunk 的层数，顺序与前向计算一致
--num-layers-to-build  ***
```

## ZB-H1 流水线

通过拆分参数/激活值梯度计算减少流水线气泡，显存占用与 1f1b 相同，在小 batch 场景下训练性能有明显提升：

```bash
--schedule-method zb_h1
--delay-wgrad-compute              # zb_h1 自动开启，可省略
```

> 注意：需满足流水线 stage 数大于 1；不支持开启 vp。

## 1f1b cooldown 阶段优化

对 1f1b 流水线 cooldown 阶段的参数/激活值梯度计算进行拆分，提升小 batch 场景训练性能：

```bash
--delay-1f1b-cooldown-wgrad-compute
--delay-wgrad-compute              # 使用上述参数时自动开启，可省略
```

> 注意：需满足流水线 stage 数大于 1；不支持开启 vp。

## Seq1F1B 长序列流水线

Seq1F1B 是面向长序列训练的高效流水线调度算法，将批次级别的调度单元分解为序列级别，改善工作负载平衡并降低显存占用。在 64 个 A100 GPU 上可训练 300 亿参数模型，最大序列长度达 64k（无需重计算）。

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `--pipe-sp-strategy` | str | `uniform_comp` | 序列切割方式：`uniform_comp`（按计算量均衡切割，每段 seq 非等长）或 `average`（均匀切割） |
| `--pipe-sp-splits` | int | `1` | seq 切分段数，由显存决定；保证最大显存利用的同时尽量减小切分段数（更多切分会增加迭代时长） |
| `--use-flash-attn` | bool | `true` | 使用 seq1f1b 时必须开启 |
| `--schedule-method` | str | `seq1f1b` | 使用 seq1f1b 时必须设置；还支持 `interleaved_seg1f1b` |

> 特别说明：
> - Seq1F1B 暂不支持激活值重计算
> - 不支持 transformer engine
> - 仅支持 mcore + local 或 legacy + local 方式
> - 推荐 `uniform_comp + seq1f1b` 组合
