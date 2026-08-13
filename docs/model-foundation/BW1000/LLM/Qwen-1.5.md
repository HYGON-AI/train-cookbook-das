# Qwen1.5

## 模型简介

Qwen1.5 是阿里通义千问第一代大语言模型，支持 14B ~ 32B 多种参数规模。

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
      <th rowspan="2">示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen1.5-14B">Qwen1.5-14B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen1.5">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen1.5-32B">Qwen1.5-32B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>16</td>
      <td><=4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/qwen1.5">✅</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Qwen1.5 原生支持 BF16，在 HCU 上运行稳定