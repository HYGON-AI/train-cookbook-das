# Qwen3-VL

## 模型简介

Qwen3-VL 是阿里通义千问第三代视觉多模态理解模型，支持 2B ~ 235B 多种参数规模。

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
      <td>qwen3-VL-2B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen3-VL-4B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen3-VL-8B</td>
      <td>8</td><td>bf16</td>
      <td>1</td><td>64</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>1</td>
      <td>1638</td>
      <td><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
    </tr>
    <tr>
      <td>qwen3-VL-32B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen3-VL-30B-A3B</td>
      <td>32</td><td>bf16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>3150</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen3-VL-235B-A22B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen3-VL 原生支持 bf16，在 DCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高 