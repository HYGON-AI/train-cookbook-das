# MiniMax-H3 · BW1000 微调

## 环境配置

推荐镜像启动训练，可参考 [DiffSynth-Studio HCU 环境配置](../../../framework/diffsynthstudio.md#hcu-环境配置) 进行容器建立、代码克隆等

## 模型权重准备

按 ModelScope 模型目录格式，将 MiniMax-H3 权重组织目录结构如下：

```text
path/to/models/
└── MiniMax/
    └── MiniMax-H3/
        └── Ref2VA/
            ├── transformer/
            ├── text_encoder/
            ├── video_vae/
            ├── audio_vae/
            └── processor/
            ……
```

## 运行
修改 `examples-hcu/MiniMax-H3/**/MiniMax-H3-Ref2VA.sh` 中的 `DIFFSYNTH_MODEL_BASE_PATH` 为容器内模型根目录的绝对路径`path/to/models/`，直接运行以下命令即可。

### Ref2VA LoRA 微调（单机 8 卡）

```bash
cd /data/DiffSynth-Studio-das
DIFFSYNTH_FA_GPU_CACHE_LAYERS=50 bash examples-hcu/MiniMax-H3/lora/MiniMax-H3-Ref2VA.sh
```
### Ref2VA 全量 微调（单机 8 卡）

```bash
cd /data/DiffSynth-Studio-das
DIFFSYNTH_CPU_ADAM_PIPELINE=fused DIFFSYNTH_FA_GPU_CACHE_LAYERS=20 bash examples-hcu/MiniMax-H3/full/MiniMax-H3-Ref2VA.sh
```
> **注：** 以上脚本均已固定随机种子（seed=42），并预设了训练所需的主要参数，可直接用于复现实验结果。如需调整训练配置，可在脚本中修改对应参数。

