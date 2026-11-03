# GLM-5

## 模型简介

GLM-5 是智谱开源的大语言模型。SLIME-DAS 当前在 BW1000 上提供裁剪为 4 层的 GRPO 功能验证示例，用于验证 Megatron-LM Actor、SGLang rollout 和在线权重更新链路。

## 推荐镜像

```text
harbor.sourcefind.cn:5443/dcu/admin/base/custom:slime-das-ubuntu22.04-dtk26.04-py3.10-20260807
```

## 模型列表

<table>
  <thead>
    <tr>
      <th>模型</th>
      <th>Training Algorithm</th>
      <th>Rollout backend</th>
      <th>Train backend</th>
      <th>推荐卡数</th>
      <th>最大响应长度</th>
      <th>示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GLM-5（4 层）</td>
      <td>GRPO</td>
      <td>SGLang</td>
      <td>Megatron-LM</td>
      <td>8（Actor 4 + Rollout 4）</td>
      <td>64</td>
      <td align="center"><a href="https://github.com/HYGON-AI/slime-das/blob/main/hcu_example/run_glm5_4layer.sh">✅</a></td>
    </tr>
  </tbody>
</table>

## 备注

当前脚本仅使用裁剪后的 4 层模型进行软件链路功能验证，不代表完整 GLM-5 模型已经完成兼容性、精度或性能验证，也不能作为完整模型的性能基准。
