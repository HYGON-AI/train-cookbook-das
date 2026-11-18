# Qwen2/2.5

## 模型简介

Qwen2 和 Qwen2.5 是阿里通义千问第二代大语言模型，支持 0.5B ~ 72B 多种参数规模。

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
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2-0.5B">Qwen2-0.5B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2-1.5B">Qwen2-1.5B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2-7B">Qwen2-7B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2-72B">Qwen2-72B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>16</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-0.5B">Qwen2.5-0.5B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-1.5B">Qwen2.5-1.5B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-3B">Qwen2.5-3B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-7B">Qwen2.5-7B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-14B">Qwen2.5-14B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-32B">Qwen2.5-32B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-72B">Qwen2.5-72B</a></td>
      <td>megatron-lm</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>16</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.19.2/examples/qwen2">link</a></td>
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

- Qwen2 和Qwen2.5 原生支持 bf16，在 HCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
