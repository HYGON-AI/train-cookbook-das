# Qwen3-VL

## 模型简介

Qwen3-VL 是阿里通义千问第三代视觉多模态理解模型，支持 2B ~ 235B 多种参数规模。

## 推荐镜像
docker pull harbor.sourcefind.cn:5443/dcu/admin/base/custom:pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10

## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">精度</th>
      <th rowspan="2">torch版本</th>
      <th rowspan="2">TE版本</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本<qwen/th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Qwen3-VL-2B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen3-VL-4B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-VL-8B-Instruct/files">Qwen3-VL-8B</a></td>
       <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-VL-32B-Instruct/files">Qwen3-VL-32B</a></td>
       <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-VL-30B-A3B-Instruct/files">Qwen3-VL-30B-A3B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td>Qwen3-VL-235B-A22B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Qwen3-VL 原生支持 bf16，在 HCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高 