# Gemma-3

## 模型简介

Gemma-3VL 是google开源的大语言模型, 语言模型有 4-27B 参数。

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
      <td><a href="https://www.modelscope.cn/models/google/gemma-3-4b-it/files">Gemma 3-4B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/gemma3">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/google/gemma-3-12b-it/files">Gemma 3-12B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-LM-das/tree/core_v0.18.2/examples/gemma3">✅</a></td>
    </tr>
    <tr>
      <td>Gemma 3-27B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Gemma-3 原生支持 bf16，在 HCU 上运行稳定
- Gemma-3 只有1B是语言模型, 其他版本都是多模态模型