# Qwen2/2.5

## 模型简介

Qwen2 和 Qwen2.5 是阿里通义千问第二代大语言模型，支持 0.5B ~ 72B 多种参数规模。

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
      <td>Qwen2-0.5B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2-1.5B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2-7B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2-72B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2.5-0.5B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2.5-1.5B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-3B">Qwen2.5-3B</a></td>
      <td>FP16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=16384</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-7B">Qwen2.5-7B</a></td>
      <td>FP16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=16384</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-14B">Qwen2.5-14B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>16</td>
      <td><=16384</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen2.5-32B</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-72B">Qwen2.5-72B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>32</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/qwen2">✅</a></td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen2 和Qwen2.5 原生支持 bf16，在 DCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
