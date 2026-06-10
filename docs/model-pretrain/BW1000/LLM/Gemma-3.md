# Gemma-3

## 模型简介

Gemma-3 是google开源的大语言模型, 语言模型有 1B 参数。

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
      <td>Gemma 3-1B</td>
      <td>8</td><td>bf16</td>
      <td>1</td><td>32</td><td>4096</td>
      <td>1</td><td>1</td><td>-</td><td>-</td><td>1</td>
      <td>10549</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/gemma3">✅</a></td>
    </tr>
    <tr>
      <td>-</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Gemma-3 原生支持 bf16，在 DCU 上运行稳定
- Gemma-3 只有1B是语言模型, 其他版本都是多模态模型