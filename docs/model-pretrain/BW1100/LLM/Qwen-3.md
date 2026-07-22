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
      <td>2</td><td>1</td><td>-</td><td>-</td><td>1</td>
      <td>1796</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-8b-dcu8-b32-seq32k.log">bw1100(1796)</a>:<a href="./logs/Qwen3-8B-h20_8-b32-s32768.log">h20(1705)</a>=105%</td>
    </tr>
    <tr>
      <td>qwen3-8B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>8192</td>
      <td>1</td><td>1</td><td>-</td><td>-</td><td>1</td>
      <td>3085</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
       <td align="center"><a href="./logs/Qwen3-8b-dcu8-b32-seq8192.log">bw1100(3085)</a>:<a href="./logs/Qwen3-8B-h20_8-b32-s8192.log">h20(2445)</a>=126%</td>
    </tr>
    <tr>
      <td>qwen3-14B</td>
      <td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td><td>-</td><td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>qwen3-32B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>4096</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>812</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
       <td align="center"><a href="./logs/Qwen3-32b-dcu8-b32-seq4096.log">bw1100(812)</a>:<a href="./logs/Qwen3-32B-h20_8-b32-s4096.log">h20(573)</a>=142%</td>
    </tr>
    <tr>
      <td>qwen3-32B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>64</td><td>8192</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>709</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
       <td align="center"><a href="./logs/Qwen3-32b-dcu32-b64-seq8192.log">bw1100(709)</a></td>
    </tr>
    <tr>
      <td>qwen3-32B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>256</td><td>8192</td>
      <td>2</td><td>1</td><td>-</td><td>-</td><td>2</td>
      <td>783</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
       <td align="center"><a href="./logs/Qwen3-32b-dcu32-b256-seq8192.log">bw1100(783)</a></td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>4096</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>2776</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-30ba3b-dcu8-b32-seq4096.log">bw1100(2776)</a>:<a href="./logs/Qwen3-30B-A3B-h20_8-b32-s4096-new.log">h20(3743)</a>=74%</td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>8</td><td>BF16</td>
      <td>2</td><td>32</td><td>4096</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>3251</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-30ba3b-dcu8-b32-seq4096-mbs2.log">bw1100(3251)</a></td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>128</td><td>4096</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>2201</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-30ba3b-dcu32-b128-seq4096.log">bw1100(2201)</a></td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>32</td><td>BF16</td>
      <td>2</td><td>128</td><td>4096</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>2869</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-30ba3b-dcu32-b128-seq4096-mbs2.log">bw1100(2869)</a></td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>8</td><td>BF16</td>
      <td>1</td><td>32</td><td>8192</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>2780</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-30ba3b-dcu8-b32-seq8192.log">bw1100(2780)</a>:<a href="./logs/Qwen3-30B-A3B-h20_8-b32-s8192.log">h20(2566)</a>=108%</td>
    </tr>
    <tr>
      <td>qwen3-30B-A3B</td>
      <td>32</td><td>BF16</td>
      <td>1</td><td>128</td><td>8192</td>
      <td>1</td><td>1</td><td>1</td><td>8</td><td>1</td>
      <td>2359</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.17.0/examples/qwen3">✅</a></td>
      <td align="center"><a href="./logs/Qwen3-30ba3b-dcu32-b128-seq8192.log">bw1100(2359)</a></td>
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
