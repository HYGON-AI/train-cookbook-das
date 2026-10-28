# Gemma-4

## 模型简介

Gemma-4 是google开源的大语言模型，提供了多种参数规模。

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
      <td><a href="https://www.modelscope.cn/models/google/gemma-4-E4B-it">Gemma 4-E4B-text</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>10.16.1.152:5000/jenkins/model_test_env/megatron:0.18.2-ubuntu22.04-dtk2610-py3.12-20260928-1056</a></td>
      <td>16</td>
      <td><=4096</td>
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

- Gemma-4 支持 bf16，在 HCU 上运行稳定
- Gemma-4 E4B是dense模型，由于PLE层，不允许开启PP和SP
