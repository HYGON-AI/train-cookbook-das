# DeepSeek-V3

## 模型简介

DeepSeek-V3 是一个开源的MoE大语言模型, 有 671B 参数规模。

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
      <td>DeekSeek V3-671B</td>
      <td>1024</td><td>bf16</td>
      <td>1</td><td>2048</td><td>4096</td>
      <td>4</td><td>1</td><td>1</td><td>64</td><td>8</td>
      <td>210</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/deepseek_v3">✅</a></td>
      <td align="center"><a href="./logs/dsv3-128node.log">log</a></td>
    </tr>
    <tr>
      <td>DeekSeek V3-671B</td>
      <td>2048</td><td>bf16</td>
      <td>1</td><td>2048</td><td>4096</td>
      <td>4</td><td>1</td><td>1</td><td>64</td><td>8</td>
      <td>117</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/deepseek_v3">✅</a></td>
    </tr>
    <tr>
      <td>DeekSeek V3-671B(16层)</td>
      <td>256</td><td>bf16</td>
      <td>1</td><td>8192</td><td>4096</td>
      <td>2</td><td>1</td><td>1</td><td>64</td><td>2</td>
      <td>1664</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/deepseek_v3">✅</a></td>
      <td>vpp4+deepep+量化通信 109tflops</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- DeepSeek-V3 原生支持 bf16，在 DCU 上运行稳定
- DeepSeek-V3 只有一个671B的版本
