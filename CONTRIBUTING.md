# 贡献指南

感谢你对本仓库的关注！以下是贡献指南。

## 贡献方式

### 📝 文档贡献(PR)

最简单的贡献方式：

1. Fork 本仓库
2. 创建分支：`git checkout -b docs/your-topic`
3. 编写或修改文档
4. 提交 PR

### 🐛 问题报告(Issue)

发现错误或有改进建议？请提交 Issue，包含：

- 问题描述
- 复现步骤
- 期望行为
- 实际行为
- 环境信息（DTK 版本、硬件型号等）

## 文档规范

### 新仓库添加

- `docs/framework/` 目录下面创建新增仓库的介绍
    > 参考示例: docs/framework/hcu-megatron.md 和 docs/framework/hcu-verl.md
- `docs/` 目录下面创建新增仓库的目录, 
    > 参考示例: docs/model-foundation是megatron, docs/model-alignment是verl强化学习, 可以取一个合适的名字
- `docs/optimization/` 目录下面创建新增仓库对应的调优建议, 如果目前没有可以先空着
    > 参考示例: docs/optimization/hcu-megatron-optim
- 首页 `README` 中创建新增仓库对应的快速开始
    > 参考示例: 前两个megatron和verl的写法.

### 已有仓库的数据完善

**核心标准：别人使用你的配置和脚本，不需要问任何问题就能跑起来，并得到接近的结果。**
- 对于尚未达到最优性能的脚本, 不需要填写性能参考
- 对于已达到最优性能的脚本, 需要填写性能参考
> 参考示例：[docs\model-foundation\BW1000\LLM\Llama.md](docs\model-foundation\BW1000\LLM\Llama.md)

**❌ 不要这样做：**

- 不要定义额外的 shell 变量（除了必要的 DTK / RCCL 环境变量），否则读者需要理解变量定义才能使用命令
- 不要保留带有个人信息的代码，会干扰读者理解

**✅ 应该这样做：**

- 使用官方模型名称和参数，例如 `meta-llama/Llama-3-8B-Instruct`，不要提交非官方开源模型或自己改动后的模型(例如改变层数, 改变专家数等之后的模型)
- 仅针对以下两种 HCU 型号撰写适配文档：`BW1000`、`BW1100`，不要添加其他型号
- 对于适配的模型, 填写可运行的参数; 对于优化后的模型, 填写最佳性能参数和可复现环境信息
