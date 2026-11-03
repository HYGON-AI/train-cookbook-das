# Gemma-3-VL

## 模型简介

Gemma-3VL 是google开源的大语言模型, 语言模型有 4-27B 参数。

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
      <td><a href="https://www.modelscope.cn/models/google/gemma-3-4b-it/files">Gemma 3-4B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td><a href="https://developer.sourcefind.cn/servicelist/detail?post_id=a053d44c-b3c7-11f0-9a0f-acde48001122&active=TagDownload">pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10</a></td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/gemma3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/google/gemma-3-12b-it/files">Gemma 3-12B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td><a href="https://developer.sourcefind.cn/servicelist/detail?post_id=a053d44c-b3c7-11f0-9a0f-acde48001122&active=TagDownload">pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10</a></td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/gemma3">link</a></td>
    </tr>
    <tr>
      <td>Gemma 3-27B</td>
      <td>-</td>
      <td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
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
      <td><a href="https://www.modelscope.cn/models/google/gemma-3-4b-it/files">Gemma 3-4B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td><a href="https://developer.sourcefind.cn/servicelist/detail?post_id=a053d44c-b3c7-11f0-9a0f-acde48001122&active=TagDownload">pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10</a></td>
      <td>8</td>
      <td>4096</td>
      <td align="center"></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Gemma-3 原生支持 bf16，在 HCU 上运行稳定
- Gemma-3 只有1B是语言模型, 其他版本都是多模态模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高
