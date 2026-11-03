# Qwen3.8

## 模型简介

Qwen3.8 是阿里通义千问第三代半多模态理解模型，包含3.5的更大规模模型和qwen4前瞻的flash-next模型。

## 使用示例
1. 根据所用框架 查看对应框架的快速开始
    - [megatron-lm 快速开始](https://github.com/HYGON-AI/Megatron-LM-das/blob/core_v0.18.2/docs/getting-started.md)
    - [llamafactory 快速开始]()
    - [ms-swift 快速开始]()
    - [megatron-bridge 快速开始]()
2. 执行模型对应的脚本

## 模型列表

### 全参 预训练/sft

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">框架</th>
      <th rowspan="2">精度</th>
      <th rowspan="2">镜像</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.8-2.4T-A95B">Qwen3.8-2.4T-A95B</a></td>
      <td>Megatron-Bridge-das</td>
      <td>BF16</td><td>10.16.1.152:5000/jenkins/model_test_env/megatron:0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>128</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen38_2.4t_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.8-Flash-Next">Qwen3.8-Flash-Next</a></td>
      <td></td>
      <td></td><td></td>
      <td></td>
      <td></td>
      <td align="center"></td>
    </tr>
  </tbody>
</table>

### lora 微调

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">框架</th>
      <th rowspan="2">精度</th>
      <th rowspan="2">镜像</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td></td>
      <td></td>
      <td></td><td></td>
      <td></td>
      <td></td>
      <td align="center"></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Qwen3.5-VL 原生支持 bf16，在 HCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高
