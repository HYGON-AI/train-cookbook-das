# GLM-5.2

## 模型简介

GLM-5.2 是采用 MoE、MLA/DSA 稀疏注意力和 MTP 的大语言模型。

## 使用示例
1. 根据所用框架 查看对应框架的快速开始
    - [megatron-lm 快速开始](https://github.com/HYGON-AI/Megatron-LM-das/blob/core_v0.18.2/docs/getting-started.md)
    - [ms-swift 快速开始(暂无)]()
    - [megatron-bridge 快速开始(暂无)]()
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
      <td>GLM-5.2（7层/32专家）</td>
      <td>megatron-lm</td>
      <td>BF16</td><td><a href="http://10.16.1.152:5000/jenkins/model_test_env/mbridge:0.6.0-ubuntu22.04-dtk2604-py3.12-20260909-1017">mbridge:0.6.0-ubuntu22.04-dtk2604-py3.12-20260909-1017</a></td>
      <td>8</td>
      <td>4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/megatron-lm-dev/-/tree/3c5a399/examples/glm5_2">link</a></td>
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
      <td>GLM-5.2（7层/32专家）</td>
      <td>megatron-bridge</td>
      <td>BF16</td><td><a href="http://10.16.1.152:5000/jenkins/model_test_env/mbridge:0.6.0-ubuntu22.04-dtk2604-py3.12-20260909-1017">mbridge:0.6.0-ubuntu22.04-dtk2604-py3.12-20260909-1017</a></td>
      <td>8</td>
      <td>4096</td>
      <td align="center"></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- 当前性能记录使用 7 层、32 专家的验证配置
- DSA 使用 HIP 后端，MoE 使用 DeepEP
