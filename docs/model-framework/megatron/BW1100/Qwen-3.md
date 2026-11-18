# Qwen3

## 模型简介

Qwen3 是阿里通义千问第三代大语言模型，支持 0.6B ~ 235B 多种参数规模。

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
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-0.6B">Qwen3-0.6B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>8192</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-1.7B">Qwen3-1.7B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>8192</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-4B">Qwen3-4B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>8192</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-8B">Qwen3-8B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>32768</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-14B">Qwen3-14B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-32B">Qwen3-32B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>32</td>
      <td>8192</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-30B-A3B">Qwen3-30B-A3B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>8192</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">link</a></td>
    </tr>
    <tr>
      <td>qwen3-235B-A22B</td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>128</td>
      <td>4096</td>
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
  </tbody>
</table>

## HCU 适配注意

- Qwen3 原生支持 bf16，在 HCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
