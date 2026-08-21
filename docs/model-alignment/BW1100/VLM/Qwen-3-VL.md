# Qwen3

## 模型简介

Qwen3 是阿里通义千问第二代大语言模型，支持多种参数规模。

## 推荐镜像

https://developer.sourcefind.cn/servicelist/detail?post_id=61036870-b3c7-11f0-9989-acde48001122&active=Overview

## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">Training Algorithm</th>
      <th rowspan="2">精度</th>
      <th colspan="3" style="text-align:center">环境依赖</th>
      <th rowspan="2">Train backend</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本</th>
    </tr>
    <tr>
        <th align="center">torch版本</th>
        <th align="center">TE版本</th>
        <th align="center">VLLM/sglang版本</th>
    </rt>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-VL-8B-Instruct">Qwen3vl-8B</a></td>
      <td>grpo</td>
      <td>-</td>
      <td>-</td><td>-</td><td>vllm</td>
      <td>FSDP2, Megatron</td>
      <td>-</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/HYGON-AI/verl-das/tree/main/examples/grpo_trainer">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-VL-8B-Instruct">Qwen3vl-8B</a></td>
      <td>on_policy_distillation</td>
      <td>-</td>
      <td>-</td><td>-</td><td>vllm</td>
      <td>FSDP</td>
      <td>-</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/HYGON-AI/verl-das/tree/main/examples/grpo_trainer">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen3-VL-8B-Instruct">Qwen3vl-8B</a></td>
      <td>multi_on_policy_distillation</td>
      <td>-</td>
      <td>-</td><td>-</td><td>vllm</td>
      <td>FSDP, VeOmni</td>
      <td>-</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/HYGON-AI/verl-das/tree/main/examples/grpo_trainer">✅</a></td>
    </tr>
  </tbody>
</table>
