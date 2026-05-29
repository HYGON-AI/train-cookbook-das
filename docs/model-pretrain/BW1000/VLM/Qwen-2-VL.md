# Qwen2/2.5-VL

## 模型简介

Qwen2/2.5-VL 是阿里通义千问第二代视觉多模态理解模型，支持 2B ~ 72B 多种参数规模。

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
      <th rowspan="2">备注</th>
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
      <td>qwen2-VL-2B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen2-VL-7B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen2.5-VL-3B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen2.5-VL-7B</td>
      <td>8</td><td>bf16</td>
      <td>1</td><td>16</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>1489</td>
      <td><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen2">✅</a></td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen2.5-VL-32B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <td>qwen2.5-VL-72B</td>
      <td>128</td><td>bf16</td>
      <td>1</td><td>128</td><td>32768</td>
      <td>8</td><td>4</td><td>-</td><td>-</td><td>4</td>
      <td>225</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen2/2.5-VL 原生支持 bf16，在 DCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
- VLM模型存在前置的vision model, 对pp1的显存需求更高 