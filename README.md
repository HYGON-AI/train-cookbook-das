# train-cookbook-das

## 📖 简介

本仓库整理了在 HCU 硬件上训练、调优和运行 AI 模型的经验与最佳实践，涵盖：

- **环境搭建** — DTK 工具链、驱动安装、Python 环境配置
- **数据处理** — LLM、VLM数据处理脚本
- **模型训练** — LLM、VLM预训练、微调
- **性能优化** — 显存优化、算子调优、量化、多卡并行
- **框架适配** — Megatron-LM、Megatron-Bridge、Verl、Transformer-Engine 等
- **故障排查** — [常见问题](./docs/troubleshooting/common-issue.md)、[错误码](./docs/troubleshooting/error-codes.md)、[FAQ](./docs/troubleshooting/faq.md)
- **性能基准** — 各模型在 HCU 上的实测数据

## 📋 模型列表(绿色对勾可点击)
✅ 已验证 &nbsp;|&nbsp; 🚧 开发中 &nbsp;|&nbsp; `-` 暂未验证
<table align="center">
  <thead>
    <tr>
      <th rowspan="2">类型</th>
      <th rowspan="2">模型</th>
      <th colspan="2" style="text-align:center">PreTrain/SFT</th>
      <th colspan="2" style="text-align:center">RL/DPO</th>
    </tr>
    <tr>
      <th align="center">BW1000</th>
      <th align="center">BW1100</th>
      <th align="center">BW1000</th>
      <th align="center">BW1100</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="14">Large Language Models (LLM)</td>
      <td>DeepSeek v3</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/DeepSeek-3.md">✅</a></td>
      <td align="center"><a href="docs/model-foundation/BW1100/LLM/DeepSeek-3.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 2</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 3</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/Gemma-3.md">✅</a></td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 4</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>GLM-4.5</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>GLM-5</td>
      <td align="center">🚧</td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>GPT-3</td>
      <td align="center">🚧</td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>GPT-oss</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Kimi K2</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Llama 2/3</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/Llama.md">✅</a></td>
      <td align="center"><a href="docs/model-foundation/BW1100/LLM/Llama.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 1.5</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/Qwen-1.5.md">✅</a></td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 2/2.5</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/Qwen-2.md">✅</a></td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-alignment/BW1100/LLM/Qwen-2.md">✅</a></td>
    </tr>
    <tr>
      <td>Qwen 3</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/Qwen-3.md">✅</a></td>
      <td align="center"><a href="docs/model-foundation/BW1100/LLM/Qwen-3.md">✅</a></td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-alignment/BW1100/LLM/Qwen-3.md">✅</a></td>
    </tr>
    <tr>
      <td>Qwen3-Next</td>
      <td align="center"><a href="docs/model-foundation/BW1000/LLM/Qwen3-Next.md">✅</a></td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
  <tbody>
    <tr>
      <td rowspan="6">Vision Language Models (VLM)</td>
      <td>Gemma 3-VL</td>
      <td align="center"><a href="docs/model-foundation/BW1000/VLM/Gemma-3-VL.md">✅</a></td>
      <td align="center">🚧</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 4-VL</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>GLM 4.5-VL</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 2/2.5-VL</td>
      <td align="center"><a href="docs/model-foundation/BW1000/VLM/Qwen-2-VL.md">✅</a></td>
      <td align="center"><a href="docs/model-foundation/BW1100/VLM/Qwen-2-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 3-VL</td>
      <td align="center"><a href="docs/model-foundation/BW1000/VLM/Qwen-3-VL.md">✅</a></td>
      <td align="center"><a href="docs/model-foundation/BW1100/VLM/Qwen-3-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-alignment/BW1100/VLM/Qwen-3-VL.md">✅</a></td>
    </tr>
    <tr>
      <td>Qwen 3.5-VL</td>
      <td align="center"><a href="docs/model-foundation/BW1000/VLM/Qwen-3.5-VL.md">✅</a></td>
      <td align="center"><a href="docs/model-foundation/BW1100/VLM/Qwen-3.5-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## 快速开始
在HCU上跑一个AI模型模型，请参考
- [Megatron-LM-das-快速开始](https://github.com/HYGON-AI/Megatron-LM-das)。
- [Verl-das-快速开始](https://github.com/HYGON-AI/verl-das)。

## 📄 许可证与第三方来源

本项目采用 [MIT License](LICENSE)。

仓库不直接内嵌第三方源码。文档中引用的模型、推理框架、工具和服务仍由各自项目的许可证约束，具体说明见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。



## 🤝 贡献

欢迎提交 Issue 和 PR！详见 [CONTRIBUTING.md](CONTRIBUTING.md)。
