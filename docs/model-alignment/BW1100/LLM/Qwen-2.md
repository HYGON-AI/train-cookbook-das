# Qwen2/2.5

## 模型简介

Qwen2 和 Qwen2.5 是阿里通义千问第二代大语言模型，支持 0.5B ~ 72B 多种参数规模。

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
      <td>Qwen2-0.5B</td>
      <td>-</td>
      <td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2.5-0.5B</td>
      <td>grpo</td>
      <td>-</td>
      <td>-</td><td>-</td><td>vllm</td>
      <td>FSDP</td>
      <td>-</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/HYGON-AI/verl-das/tree/main/examples/grpo_trainer">✅</a></td>
    </tr>
    <tr>
      <td>Qwen2.5-0.5B</td>
      <td>fully_async_policy</td>
      <td>-</td>
      <td>-</td><td>-</td><td>vllm</td>
      <td>FSDP2</td>
      <td>-</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/HYGON-AI/verl-das/tree/main/examples/grpo_trainer">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-7B">Qwen2.5-7B</a></td>
      <td>fully_async_policy</td>
      <td>-</td>
      <td>-</td><td>-</td><td>vllm</td>
      <td>FSDP2</td>
      <td>-</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/HYGON-AI/verl-das/tree/main/examples/grpo_trainer">✅</a></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-14B">Qwen2.5-14B</a></td>
      <td>-</td>
      <td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td>Qwen2.5-32B</td>
      <td>-</td>
      <td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/Qwen/Qwen2.5-72B">Qwen2.5-72B</a></td>
      <td>-</td>
      <td>-</td>
      <td>-</td><td>-</td><td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td align="center">正在适配</td>
    </tr>
  </tbody>
</table>
