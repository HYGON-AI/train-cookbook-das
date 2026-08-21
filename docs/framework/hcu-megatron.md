# hcu-megatron on HCU

> 本文档介绍 hcu-megatron 框架的基本信息、安装方式与集成方法。具体的调优特性与使用方法请参考 [optimization/hcu-megatron-optim](../optimization/README.md#hcu-megatron-专项调优)。

## 简介

hcu-megatron 是面向 HCU 环境的 Megatron-LM 增强库，通过替换 Megatron 的函数或类，引入新特性或实现更好的训练性能。核心能力包括：

- **流水线并行优化**：支持 interleaved 1f1b MoE A2A overlap、DualPipeV、ZB-H1、RiPipe 等多种高效流水线调度策略
- **显存优化**：支持激活函数重计算、异步激活值 offload、参数副本复用、指定层重计算等多种显存节省手段
- **通信优化**：支持基于 Flux 的 TP 计算通信 overlap、all2all 量化通信（int4/int8）、EDGC 动态梯度压缩
- **长序列训练**：支持 Seq1F1B 序列级流水线调度，可在不使用重计算的情况下训练 64k 长序列
- **模型扩展**：通过 Megatron-Bridge 支持更多 HuggingFace 模型架构直接接入 Megatron 训练
- **MHC**：支持 Hyper Connections（多残差流）特性，提供 torch 原生和 tile_kernel 两种实现

源码仓库：<https://github.com/HYGON-AI/Megatron-LM-das>

## 版本依赖

- dtk >= 25.04
- transformer-engine >= 2.4.0
- torch >= 2.6.0

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
# num_nodes 为运行的节点数，默认 8 卡/机
bash run_deepseekv3_671B.sh hostfile_deepseekv3_671B num_nodes
```

## 调优特性

hcu-megatron 提供的具体调优特性与使用方法按类别整理如下：

- [**流水线并行**](../optimization/hcu-megatron-optim/pipeline-parallel.md) — interleaved 1f1b MoE A2A overlap、DualPipeV、ZB-H1、1f1b cooldown 拆分、Seq1F1B 长序列流水线
- [**重计算优化**](../optimization/hcu-megatron-optim/recompute.md) — RiPipe 重计算独立调度、激活函数重计算、指定层重计算
- [**显存优化（Offload 与参数复用）**](../optimization/hcu-megatron-optim/memory-offload.md) — 参数副本复用（FP32 → BF16 + 残差）、异步激活值 Offload
- [**通信优化**](../optimization/hcu-megatron-optim/communication.md) — 张量并行 Flux 加速、all2all 量化通信、EDGC 动态梯度压缩
- [**Checkpoint 加速**](../optimization/hcu-megatron-optim/checkpoint.md) — 内存缓存 Checkpoint（hyckpt）
- [**模型特性扩展**](../optimization/hcu-megatron-optim/model-features.md) — MHC 超连接、Megatron-Bridge
