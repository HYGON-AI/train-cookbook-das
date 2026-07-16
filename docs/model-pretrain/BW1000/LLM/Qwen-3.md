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
      <td>qwen3-0.6B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-1.7B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-4B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-8B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>32768</td>
      <td>2</td><td>4</td><td>-</td><td>-</td><td>1</td>
      <td>1765</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-8B-dcu8-b32-s32768.log">log</a></td>
    </tr>
      <tr>
      <td>qwen3-8B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>8192</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>1</td>
      <td>3467</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-8B-dcu8-b32-s8192.log">log</a></td>
    </tr>
    <tr>
      <td>qwen3-14B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>1927</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-14B-dcu8-b32-s4096.log" target="_blank">log</a>
    </tr>
    <tr>
      <td>qwen3-32B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>64</td><td>8192</td>
      <td>4</td><td>1</td><td>-</td><td>-</td><td>4</td>
      <td>748</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-32B-dcu32-b64-s8196.log">log</a></td>
    </tr>
    <tr>
      <td>qwen3-32B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>64</td><td>8192</td>
      <td>4</td><td>1</td><td>-</td><td>-</td><td>4</td>
      <td>815</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-32B-dcu32-b256-s8196.log">log</a></td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>64</td><td>8192</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>4</td>
      <td>2353</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-235B-A22B</td>
      <td>128</td><td>bf16</td>
      <td>1</td><td>128</td><td>4096</td>
      <td>4</td><td>2</td><td>1</td><td>8</td><td>16</td>
      <td>292</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## DCU 适配注意

- Qwen3 原生支持 bf16，在 DCU 上运行稳定
- MoE 模型的激活参数很小，实际显存需求低于同等 dense 模型
