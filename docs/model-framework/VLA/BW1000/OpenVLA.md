# OpenVLA

## 模型简介

OpenVLA 是 7B 规模的开源视觉-语言-动作（VLA）模型，基于 Prismatic VLM（DINOv2 + SigLIP 视觉编码器与 Llama-2 7B 语言模型）构建，把机器人操作观测和语言指令映射为离散化的 7 自由度动作 token，支持在 BridgeData V2 等操作数据集上进行全参数微调。


## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">精度</th>
      <th colspan="1" style="text-align:center">环境版本</th>
      <th colspan="3" style="text-align:center">推荐训练参数</th>
      <th rowspan="2">示例脚本</th>
    </tr>
    <tr>
      <th>torch</th>
      <th>Batch Size</th>
      <th>Global Batch Size</th>
      <th>Step</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>OpenVLA</td>
      <td>8</td>
      <td>BF16</td>
      <td>2.10.0</td>
      <td>32</td>
      <td>256</td>
      <td>1000</td>
      <td><a href="https://github.com/HYGON-AI/TurboPhysAI/tree/main/model_examples/OpenVLA">✅</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- OpenVLA 原生支持 BF16 混合精度，在 HCU 上运行稳定
- 构建 OpenVLA 训练环境可参考<a href="https://github.com/HYGON-AI/TurboPhysAI/tree/main/model_examples/OpenVLA">训练环境构建说明</a>

