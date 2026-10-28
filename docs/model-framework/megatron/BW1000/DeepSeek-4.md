# DeepSeek-V4

## 模型简介

DeepSeek-V4 是一个开源的MoE大语言模型, 有 pro(1.6T-A49B) 和 flash(284B-A13B)两个版本。

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
      <td><a href="https://www.modelscope.cn/models/deepseek-ai/DeepSeek-V4-Flash">DeepSeek-V4-Flash</a></td>
      <td>Megatron-Bridge-das</td>
      <td>BF16</td><td><a href="10.16.1.152:5000/jenkins/model_test_env/megatron:0.19.2-ubuntu22.04-dtk2610-py3.12-1009">10.16.1.152:5000/jenkins/model_test_env/megatron:0.19.2-ubuntu22.04-dtk2610-py3.12-1009</a></td>
      <td>32(6层)</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/deepseek/train_deepseekv4_flash_pretrain.sh">link</a></td>
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
      <td><a href="https://www.modelscope.cn/models/deepseek-ai/DeepSeek-V4-Flash">DeepSeek-V4-Flash</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td><a href="https://developer.sourcefind.cn/servicelist/detail?post_id=a053d44c-b3c7-11f0-9a0f-acde48001122&active=TagDownload">pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10</a></td>
      <td>1024</td>
      <td>4096</td>
      <td align="center">sft</td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- DeepSeek-V3 原生支持 bf16，在 HCU 上运行稳定
- DeepSeek-V3 只有一个671B的版本
