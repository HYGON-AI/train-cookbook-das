# DCU train Cookbook

## 📖 简介

本仓库整理了在 DCU 硬件上部署、调优和运行 AI 模型的经验与最佳实践，涵盖：

- **环境搭建** — DTK 工具链、驱动安装、Python 环境配置
- **数据处理** — LLM、VLM数据处理脚本
- **模型训练** — LLM、VLM预训练、微调
- **性能优化** — 显存优化、算子调优、量化、多卡并行
- **框架适配** — Megatron-LM、Megatron-Bridge、Transformers、Transformer-Engine 等
- **故障排查** — 常见问题、错误码、FAQ
- **性能基准** — 各模型在 DCU 上的实测数据

## 📋 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">类型</th>
      <th rowspan="2">模型</th>
      <th colspan="3" style="text-align:center">预训练</th>
      <th colspan="3" style="text-align:center">微调</th>
    </tr>
    <tr>
      <th align="center">K100_AI</th>
      <th align="center">BW1000</th>
      <th align="center">BW1100</th>
      <th align="center">K100_AI</th>
      <th align="center">BW1000</th>
      <th align="center">BW1100</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="13">Large Language Models (LLM)</td>
      <td>-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>DeepSeek v3</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/DeepSeek-3.md">✅</a></td>
      <td align="center"><a href="docs/model-pretrain/BW1100/LLM/DeepSeek-3.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 2</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 3</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/Gemma-3.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 4</td>
      <td align="center">-</td>
      <td align="center">-</td>
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
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>GPT-oss</td>
      <td align="center">-</td>
      <td align="center">-</td>
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
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Llama 2/3</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/Llama.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 1.5</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/Qwen-1.5.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 2/2.5</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/Qwen-2.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-finetune/BW1000/LLM/Qwen-2.md">✅</a></td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 3</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/Qwen-3.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-finetune/BW1100/LLM/Qwen-3.md">✅</a></td>
    </tr>
    <tr>
      <td>Qwen3-Next</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/LLM/Qwen3-Next.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="6">Vision Language Models (VLM)</td>
      <td>Gemma 3-VL</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/VLM/Gemma-3-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Gemma 4-VL</td>
      <td align="center">-</td>
      <td align="center">-</td>
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
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>Qwen 2/2.5-VL</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/VLM/Qwen-2-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-finetune/BW1100/VLM/Qwen-2-VL.md">✅</a></td>
    </tr>
    <tr>
      <td>Qwen 3-VL</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/VLM/Qwen-3-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-finetune/BW1100/VLM/Qwen-3-VL.md">✅</a></td>
    </tr>
    <tr>
      <td>Qwen 3.5-VL</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-pretrain/BW1000/VLM/Qwen-3.5-VL.md">✅</a></td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## 🤝 贡献

欢迎提交 Issue 和 PR！详见 [CONTRIBUTING.md](CONTRIBUTING.md)。
