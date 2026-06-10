# Qwen3

## 模型简介

Qwen3 是阿里通义千问第三代大语言模型，支持 0.6B ~ 235B 多种参数规模。

## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">测试卡数</th>
      <th rowspan="2">精度</th>
      <th colspan="3" style="text-align:center">测试参数</th>
      <th colspan="5" style="text-align:center" >测试并行策略</th>
      <th rowspan="2">吞吐量(token/s/gpu)</th>
      <th rowspan="2">测试脚本</th>
    </tr>
    <tr>
      <th >micro batch size</th>
      <th >global batch size</th>
      <th >seq length</th>
      <th >TP</th><th >CP</th><th >ETP</th><th >EP</th><th >PP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>qwen3-0.6B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-1.7B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-4B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">qwen3-8B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>128</td><td>32768</td>
      <td>2</td><td>2</td><td>-</td><td>-</td><td>1</td>
      <td>1745</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td>16</td><td>BF16</td>
      <td>1</td><td>128</td><td>32768</td>
      <td>2</td><td>2</td><td>-</td><td>-</td><td>1</td>
      <td>1743</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td>qwen3-14B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-32B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">qwen3-30B-A3B</td>
      <td>16</td><td>BF16</td>
      <td>1</td><td>128</td><td>8192</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>2934</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td>16</td><td>BF16</td>
      <td>2</td><td>128</td><td>4096</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>3338</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td>qwen3-235B-A22B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen3 原生支持 bf16，在 DCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
