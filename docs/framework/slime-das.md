# SLIME-DAS on HCU

## 简介

SLIME-DAS 是基于 [THUDM/slime](https://github.com/THUDM/slime) 的 HCU 平台适配版本，用于基于 Megatron-LM 和 SGLang 的大规模强化学习训练。

SLIME-DAS 提供 HCU 平台训练和 rollout、Ray 分布式资源调度、SGLang rollout 服务、Megatron-LM Actor 训练，以及通过 Megatron-Bridge 加载 Hugging Face 模型权重的能力。

仓库地址：<https://github.com/HYGON-AI/slime-das>

## 环境与安装

运行环境需要 Linux、Python 3.10 或更高版本，以及已安装 HCU 运行时、HCU 版本 PyTorch、SGLang、Megatron-LM 和 Megatron-Bridge 的基础镜像。

推荐镜像：

```text
harbor.sourcefind.cn:5443/dcu/admin/base/custom:slime-das-ubuntu22.04-dtk26.04-py3.10-20260807
```

```bash
git clone https://github.com/HYGON-AI/slime-das.git
cd slime-das
python -m pip install -r requirements.txt
```

设置外部组件路径：

```bash
export MEGATRON_BRIDGE_ROOT=<path-to-megatron-bridge>
export MEGATRON_LM_ROOT=<path-to-megatron-lm>
export SGLANG_ROOT=<path-to-sglang>
```

## 快速开始

准备 Qwen3-4B、DAPO-Math-17k 和 AIME 2024 后，可在单节点上启动 Ray 和 GRPO 训练：

```bash
cd hcu_example
source common_env.sh
NUM_GPUS=8 bash start_ray.sh <node-ip>

MODEL_PATH=<path-to-qwen3-4b> \
DATA_ROOT=<path-to-data-root> \
SAVE_ROOT=<path-to-checkpoint-output> \
NODE_IP=<node-ip> \
SUBMIT_MODE=direct \
bash run_qwen3_4b.sh
```

`DATA_ROOT` 下应包含 `dapo-math-17k/dapo-math-17k.jsonl` 和 `aime-2024/aime-2024.jsonl`。多节点运行时，在 head 节点启动 Ray、让 worker 节点加入同一集群，再从 head 节点提交训练任务。

## 当前验证范围

- Qwen3-4B（BW1000）：[GRPO 标准训练](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_qwen3_4b.sh)和[全异步 rollout 训练](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_qwen3_4b_fully_async.sh)。
- Qwen3.5-4B（BW1000）：[模型说明](../model-framework/slime-das/BW1000/LLM/Qwen-3.5.md)与 [GRPO 训练脚本](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_qwen3.5_4b.sh)。
- GLM-5（BW1000，4 层）：[功能验证示例](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_glm5_4layer.sh)。
- DeepSeek-R1（BW1100，4 层）：[模型说明](../model-framework/slime-das/BW1100/LLM/DeepSeek-R1.md)与[功能验证脚本](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_deepseek_r1_4layer.sh)。

四层示例仅表示训练、rollout 和权重更新的软件链路已经打通，不作为完整模型兼容性或性能基准。

详细环境配置、数据准备、单机与多节点启动方式请参考 [SLIME-DAS HCU 用户指南](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/user_guide.md)。
