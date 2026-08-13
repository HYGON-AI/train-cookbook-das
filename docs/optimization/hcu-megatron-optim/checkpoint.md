# 内存缓存 Checkpoint

在大模型训练中，checkpoint 保存耗时会显著拖慢整体训练效率。hcu-megatron 支持内存缓存 ckpt，通过将 checkpoint 数据先写入内存再异步落盘，显著提升保存性能。

## 使用方式

在训练脚本中添加：

```bash
--use-ckpt-memory-cache
```

## 依赖组件

开启内存缓存 ckpt 功能后，还需要额外安装 `hyckpt` python 包并启动 `hyckptd` 后台进程：

**1. 安装 hyckpt 包：**

```bash
pip install hyckpt-1.0.1-py3-none-any.whl
```

**2. 启动 hyckptd 进程：**

```bash
mpirun -pernode -hostfile <主机名文件> hyckptd --log <日志文件路径>
```

## 注意事项

- `hyckpt` whl 包需联系相关负责人获取
- `hyckptd` 需在训练启动前先在每个节点启动
- 建议将 `hyckptd` 日志路径独立于训练日志，方便排查 ckpt 保存问题
