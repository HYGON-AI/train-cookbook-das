# 训练调优指南

本目录整理了大模型训练过程中常见的调优方式，覆盖显存优化、通信优化、流水线并行调度、精度换性能等多个维度。文档按调优场景与框架特性组织，便于根据实际瓶颈快速定位对应策略。


## 使用 hcu-megatron 训练调优

hcu-megatron 通过替换 Megatron-LM 的函数或类，引入新的特性或实现更好的性能。相关调优手段按类别整理如下：

- [**大模型训练常见调优方式**](./hcu-megatron-optim/common-optimization.md) — 通用优化（Flash Attention、通信计算 Overlap）、精度换性能（BF16 梯度规约、FP8 训练）、显存不足优化（Swap Attention、Optimizer Offload）、显存充裕优化（VP、Flux TP Overlap）、Dense/MoE 模型专项优化
- [**流水线并行**](./hcu-megatron-optim/pipeline-parallel.md) — interleaved 1f1b MoE A2A overlap、DualPipeV、ZB-H1、1f1b cooldown 拆分、Seq1F1B 长序列流水线
- [**重计算优化**](./hcu-megatron-optim/recompute.md) — RiPipe 重计算独立调度（advance / bubble）、激活函数重计算、指定层重计算
- [**显存优化（Offload 与参数复用）**](./hcu-megatron-optim/memory-offload.md) — 参数副本复用（FP32 → BF16 + 残差）、异步激活值 Offload
- [**通信优化**](./hcu-megatron-optim/communication.md) — 张量并行 Flux 加速、all2all 量化通信（int4/int8）、EDGC 动态梯度压缩
- [**Checkpoint 加速**](./hcu-megatron-optim/checkpoint.md) — 内存缓存 Checkpoint（hyckpt）
- [**模型特性扩展**](./hcu-megatron-optim/model-features.md) — MHC 超连接（torch / tile_kernel）、Megatron-Bridge（扩展 HuggingFace 模型支持）

> hcu-megatron 框架的整体安装与集成方式详见 [`../framework/hcu-megatron.md`](../framework/hcu-megatron.md)。

## 使用verl 训练调优

正在完善...