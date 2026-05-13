# Llama2/3

## 模型简介

Llama2 和 Llama3 是 Meta 开源的大语言模型，均为dense模型，支持 7B ~ 405B 多种参数规模。

## 模型列表

### 全参微调

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
      <td>llama2-7B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

### LoRA微调

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">测试卡数</th>
      <th rowspan="2">精度</th>
      <th colspan="5" style="text-align:center">测试参数</th>
      <th colspan="5" style="text-align:center" >测试并行策略</th>
      <th rowspan="2">吞吐量(token/s/gpu)</th>
      <th rowspan="2">测试脚本</th>
    </tr>
    <tr>
      <th >micro batch size</th>
      <th >global batch size</th>
      <th >seq length</th>
      <th >r</th><th >target modules</th>
      <th >TP</th><th >CP</th><th >ETP</th><th >EP</th><th >PP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>llama2-7B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Llama2 和 Llama3 原生支持 bf16，在 DCU 上运行稳定
- Llama2 和 Llama3 均为dense模型，没有moe结构
- 全参微调性能与预训练相似, LoRA微调性能受 r 和 target modules 影响较大