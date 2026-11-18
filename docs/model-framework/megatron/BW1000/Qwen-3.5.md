# Qwen3.5

## 模型简介

Qwen3.5 是阿里通义千问第三代多模态理解模型，支持 2B ~ 397B 多种参数规模。

## 使用示例
1. 根据所用框架 查看对应框架的快速开始
    - [megatron-lm 快速开始](https://github.com/HYGON-AI/Megatron-LM-das/blob/core_v0.18.2/docs/getting-started.md)
    - [llamafactory 快速开始]()
    - [ms-swift 快速开始]()
    - [megatron-bridge 快速开始](https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/docs/models/qwen/qwen3.5-text_pretrain.md)
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
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-0.8B">Qwen3.5-0.8B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen35_text_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-2B">Qwen3.5-2B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen35_text_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-4B">Qwen3.5-4B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen35_text_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-9B">Qwen3.5-9B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen35_text_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-27B">Qwen3.5-27B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen35_text_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-35B-A3B">Qwen3.5-35B-A3B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>16</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen35_text_pretrain.sh">link</a></td>
    </tr>
    <tr>
      <td>Qwen3.5-35B-A3B(sft)</td>
      <td>ms-swift</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>16</td>
      <td>256</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/main/examples/qwen/train_qwen3_vl_sft.sh">link</a></td>
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
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-9B">Qwen3.5-9B</a></td>
      <td>megatron-bridge</td>
      <td>BF16</td><td><a href="https://developer.sourcefind.cn/servicelist/detail?post_id=a053d44c-b3c7-11f0-9a0f-acde48001122&active=TagDownload">pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10</a></td>
      <td>8</td>
      <td>4096</td>
      <td align="center"></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Qwen3.5-VL 原生支持 bf16，在 HCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高
