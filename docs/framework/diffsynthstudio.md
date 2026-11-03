# DiffSynth-Studio HCU 使用指南

## 简介

DiffSynth-Studio 是由魔搭社区团队开发和维护的开源扩散模型（Diffusion）引擎，支持图像、视频和音频生成等任务。框架集成了多种主流开源模型，提供模型推理、全量训练、LoRA 微调及 Adapter 训练能力。通过动态显存管理、参数量化和拆分训练等功能，DiffSynth-Studio 可降低推理与训练的显存需求，便于开展生成式模型应用开发与研究。

## HCU 环境配置

### 拉取镜像

在 HCU 宿主机执行：

```bash
docker pull harbor.sourcefind.cn:5443/hcu/admin/base/custom:diffsynth-pytorch2100-ubuntu22.04-dtk26.04-py3.10
```

### 创建容器

以下示例将宿主机 `/data/diffsynth-workspace` 挂载到容器 `/data`，用于保存代码、模型权重、数据和训练输出。可替换宿主机路径，后续命令统一使用容器内的 `/data`。

```bash
# 创建容器
docker run -d -t   -v  /data/diffsynth-workspace:/data  -v /opt/hyhal:/opt/hyhal:ro  --workdir /data --privileged --shm-size=32G  --device=/dev/kfd --device=/dev/dri/ --device=/dev/mkfd  --network=host --group-add video  --name diffsynth-hcu  harbor.sourcefind.cn:5443/hcu/admin/base/custom:diffsynth-pytorch2100-ubuntu22.04-dtk26.04-py3.10
# 启动并进入容器
docker exec -it diffsynth-hcu bash
```

### 准备代码

进入容器后，获取 HCU 适配仓库代码并运行本地安装命令：

```bash
cd /data
git clone https://github.com/HYGON-AI/DiffSynth-Studio-das.git
cd DiffSynth-Studio-das
pip install -e .
```

### 安装必要依赖

运行以下命令安装相关依赖：

```bash
pip install pytest
```


## 支持模型

| 模型 | 平台 | 任务 |
| --- | --- | --- |
| [MiniMax-H3](../model-framework/DiffSynthStudio/BW1000/MiniMax-H3.md) | BW1000 | Ref2VA LoRA/full 微调 |
