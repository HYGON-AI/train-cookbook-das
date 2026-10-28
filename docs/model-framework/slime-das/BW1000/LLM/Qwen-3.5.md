# Qwen3.5

## 模型简介

Qwen3.5 是阿里通义千问系列大语言模型。SLIME-DAS 已在 BW1000 上提供 Qwen3.5-4B 的 GRPO 训练示例。

## 推荐镜像

```text
harbor.sourcefind.cn:5443/dcu/admin/base/custom:slime-das-ubuntu22.04-dtk26.04-py3.10-20260807
```

## 运行前准备

按照 [SLIME-DAS HCU 用户指南](https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/user_guide.md)准备 HCU 基础镜像、Megatron-LM、Megatron-Bridge、SGLang、模型权重及数据集。示例使用 DAPO-Math-17k 训练集，并使用 AIME 2024 进行评估。

## 模型列表

<table>
  <thead>
    <tr>
      <th>模型</th>
      <th>Training Algorithm</th>
      <th>精度</th>
      <th>Rollout backend</th>
      <th>Train backend</th>
      <th>推荐卡数</th>
      <th>最大响应长度</th>
      <th>示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Qwen3.5-4B</td>
      <td>GRPO</td>
      <td>BF16</td>
      <td>SGLang</td>
      <td>Megatron-LM</td>
      <td>8（Actor 4 + Rollout 4）</td>
      <td>512（示例默认值）</td>
      <td align="center"><a href="https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_qwen3.5_4b.sh">✅</a></td>
    </tr>
  </tbody>
</table>

示例可直接从 Hugging Face checkpoint 启动，也支持从 SLIME-DAS 保存目录断点续训；具体参数以仓库脚本和用户指南为准。
