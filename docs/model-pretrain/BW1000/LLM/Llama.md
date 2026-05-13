# Llama2/3

## 模型简介

Llama2 和 Llama3 是 Meta 开源的大语言模型，均为dense模型，支持 7B ~ 405B 多种参数规模。

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
      <td>llama2-7B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>1</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>4783</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/llama2">✅</a></td>
    </tr>
    <tr>
      <td>llama2-13B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>2402</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/llama2">✅</a></td>
    </tr>
    <tr>
      <td>llama2-70B</td>
      <td>64</td><td>BF16</td>
      <td>1</td><td>256</td><td>4096</td>
      <td>4</td><td>1</td><td>-</td><td>-</td><td>8</td>
      <td>510</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/llama2">✅</a></td>
    </tr>
    <tr>
      <td>llama3-8B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>64</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>1</td>
      <td>4102</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/llama3">✅</a></td>
    </tr>
    <tr>
      <td>llama3-70B</td>
      <td>64</td><td>BF16</td>
      <td>1</td><td>512</td><td>4096</td>
      <td>4</td><td>1</td><td>-</td><td>-</td><td>8</td>
      <td>423</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/llama3">✅</a></td>
    </tr>
    <tr>
      <td>llama3-405B</td>
      <td>512</td><td>BF16</td>
      <td>1</td><td>512</td><td>4096</td>
      <td>8</td><td>2</td><td>-</td><td>-</td><td>16</td>
      <td>69</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/llama3">✅</a></td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Llama2 和 Llama3 原生支持 bf16，在 DCU 上运行稳定
- Llama2 和 Llama3 均为dense模型，没有moe结构