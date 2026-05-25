# Qwen3-Next

## 模型简介

Qwen3-Next 是阿里通义千问第三代视觉多模态理解模型。

## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">测试卡数</th>
      <th rowspan="2">精度</th>
      <th colspan="3" style="text-align:center">测试参数</th>
      <th colspan="5" style="text-align:center" >测试并行策略</th>
      <th rowspan="2">吞吐量(token/s/gpu)/迭代耗时(s)</th>
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
      <td>qwen3-Next</td>
      <td>32</td><td>bf16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>2</td><td>1</td><td>1</td><td>8</td><td>4</td>
      <td>75.441s</td>
      <td>-</td>
      <td>16层</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen3-Next 原生支持 bf16，在 DCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型