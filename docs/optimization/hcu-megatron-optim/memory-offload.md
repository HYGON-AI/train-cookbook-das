# 显存优化（Offload 与参数复用）

面向单卡显存受限的场景，hcu-megatron 提供参数副本复用和异步激活值 offload 两种手段，在保持训练精度的同时降低峰值显存。

- [参数副本复用](#参数副本复用)
- [异步激活值 Offload](#异步激活值-offload)

## 参数副本复用

在大模型 BF16 训练中，通常需要保存一份 FP32 参数用于优化器更新，同时保留一份 BF16 参数用于计算。考虑到 FP32 与 BF16 参数不会同时使用，通过将 FP32 转换为 「BF16 + 残差」实现 BF16 复用，反向更新参数时基于 BF16 与残差恢复 FP32，可以额外节省一份 BF16 参数所占内存。

```bash
--use-optimizer-feature
--reuse-fp32-param
```

## 异步激活值 Offload

前向计算时将激活值异步拷贝到 CPU，反向计算前再异步拷贝回 HCU。对比重计算，将计算时间转换为异步 H2D 和 D2H 时间，可以以更少的性能损失达到相同的显存降低效果。

```bash
# 必选
--swap-attention

# 可选，控制 offload 的模块（默认 self_attention，建议只开启 self_attention）
--swap-modules input_layernorm,self_attention,post_attention_norm

# 可选，控制做 offload 的层
--specify-layers 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15
```

### 注意事项

1. 在 mcore 模式下需设置 `overlap_grad_reduce=True`
2. 依赖 transformer-engine >= 2.5
3. 建议通过 `--swap-modules` 只开启 `self_attention` 模块的 offload
4. 通过 `--specify-layers` 精确控制做 offload 的层，避免整网 offload 带来的开销
