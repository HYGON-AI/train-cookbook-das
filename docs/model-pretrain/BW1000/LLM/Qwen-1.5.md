# Qwen1.5

## 模型简介

Qwen1.5 是阿里通义千问第一代大语言模型，支持 14B ~ 32B 多种参数规模。

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
      <td>qwen1.5-14B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>4</td>
      <td>1884</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen1.5">✅</a></td>
    </tr>
    <tr>
      <td>qwen1.5-32B</td>
      <td>16</td><td>BF16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>4</td><td>1</td><td>-</td><td>-</td><td>4</td>
      <td>888</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen1.5">✅</a></td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen1.5 原生支持 bf16，在 DCU 上运行稳定