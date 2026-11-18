# GLM-5

## 模型简介

GLM-5 是采用 MoE、MLA/DSA 稀疏注意力和 MTP 的大语言模型。

## 使用示例
1. 根据所用框架 查看对应框架的快速开始
    - [megatron-lm 快速开始](https://github.com/HYGON-AI/Megatron-LM-das/blob/core_v0.18.2/docs/getting-started.md)
    - [llamafactory 快速开始]()
    - [ms-swift 快速开始]()
    - [megatron-bridge 快速开始](https://github.com/HYGON-AI/Megatron-bridge-das/blob/dev/examples_hcu/glm53_flash/README.md)
2. 执行模型对应的脚本

## 模型列表

### 全参 预训练/sft

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">框架</th>
      <th rowspan="2">精度</th>
      <th rowspan="2">镜像</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GLM-5.3-flash（24层）</td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>16</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/dev/examples_hcu/glm53_flash/train_glm53_flash_pretrain.sh">link</a></td>
    </tr>
  </tbody>
</table>

### lora 微调

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">框架</th>
      <th rowspan="2">精度</th>
      <th rowspan="2">镜像</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GLM-5.3-flash</td>
      <td>megatron-bridge</td>
      <td>BF16</td><td>harbor.sourcefind.cn:5443/hcu/admin/base/custom:megatron0.19.2-ubuntu22.04-dtk2610-py3.12-1009</td>
      <td>32</td>
      <td>4096</td>
      <td align="center"><a href="https://github.com/HYGON-AI/Megatron-bridge-das/blob/dev/examples_hcu/glm53_flash/train_glm53_flash_peft.sh">link</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- 当前记录pretrain使用 24 层的验证配置
- 当前记录lora使用全参的验证配置
- DSA 使用 HIP 后端，MoE 使用 DeepEP
