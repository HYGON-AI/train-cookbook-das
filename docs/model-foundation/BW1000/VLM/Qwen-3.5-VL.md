# Qwen3.5-VL

## 模型简介

Qwen3.5-VL 是阿里通义千问第三代纯视觉多模态理解模型，支持 2B ~ 397B 多种参数规模。

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
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-0.8B">Qwen3.5-VL-0.8B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/Qwen3.5">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-2B">Qwen3.5-VL-2B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3.5">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-4B">Qwen3.5-VL-4B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3.5">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3.5-9B">Qwen3.5-VL-9B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=2048</td>
      <td><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen3.5">✅</a></td>
    </tr>
    <tr>
      <td>Qwen3.5-VL-27B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen3.5-VL-35B-A3B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen3.5-VL-122B-A10B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen3.5-VL-397B-A17B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Qwen3.5-VL 原生支持 bf16，在 HCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高 
