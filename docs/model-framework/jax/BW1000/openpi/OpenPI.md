# OpenPI (π05)

## 模型简介

OpenPI 是 Physical Intelligence 开源的视觉-语言-动作(VLA)模型训练框架,本方案基于其中的 π05 模型,采用 JAX 实现,在 HCU 上完成 LIBERO 具身任务的微调训练。交付形式为**运行环境镜像(tar 下载 + docker load)+ 官方 OpenPI 源码 + 独立 patch + 启动脚本**,镜像只提供运行环境(不含任何 openpi 代码、权重、数据集),代码通过官方仓库 clone + patch 提供,数据集与权重由用户自行准备并挂载。

## 使用示例

1. 下载并导入运行时镜像(约 64 GB,支持断点续传,网络中断后重跑同一条命令即可):

    ```bash
    curl -f -C - -o openpi_jax010_dtk26042_v1.tar \
      https://zzefile.scnet.cn:65011/efile/s/d/cWlhbnlqMQ==/c138b78040d3e420
    docker load -i openpi_jax010_dtk26042_v1.tar
    ```

    镜像内已包含:DTK 26.04.2、与之 ABI 匹配的 JAX 栈 `0.10.0+das.opt1.dtk2604`、bs384 rocBLAS 调优库(`library_gpu5`,覆盖 62 个 GEMM 形状)、训练 pip 依赖 134 个、flax 兼容补丁。

2. 创建容器并挂载数据和权重(将 `/实际路径/...` 替换为宿主机对应目录):

    ```bash
    docker run -it --network=host --name=openpi-jax010-hcu \
      --privileged --device=/dev/kfd --device=/dev/dri \
      --ipc=host --shm-size=16G --group-add video --cap-add=SYS_PTRACE \
      -v /opt/hyhal:/opt/hyhal:ro \
      -v /实际路径/openpi-jax010-hcu:/workspace/openpi-jax010-hcu:ro \
      -v /实际路径/openpi-assets:/embodied/model/Spatialtemporal-AI/openpi-assets:ro \
      -v /实际路径/libero:/embodied/model/Spatialtemporal-AI/dataset/libero:ro \
      -v /实际路径/HF缓存:/root/.cache/huggingface/datasets/parquet \
      xuxc_jax0.10.0_openpi0.5:dtk26.04.2-jax0.10.0-v1 /bin/bash
    ```

3. 容器内 clone 官方源码并应用 patch(需联网),然后校验外部资源并启动训练:

    ```bash
    git clone https://github.com/Physical-Intelligence/openpi.git /workspace/openpi
    cd /workspace/openpi
    git checkout 215abfb217dbac7d5f1273282331b9b1866c0479
    git apply /workspace/openpi-jax010-hcu/patches/0100-openpi-hcu-jax010-runtime.patch

    # 容器内初始化(每次新建容器执行一次):tokenizer 通过 gs://big_vision/... 解析,需要该软链
    ln -sfn /embodied/model/Spatialtemporal-AI/openpi-assets/big_vision \
            /embodied/model/Spatialtemporal-AI/big_vision

    # 校验外部资源(不联网)
    MODEL_ROOT=/embodied/model/Spatialtemporal-AI \
    DATA_ROOT=/embodied/model/Spatialtemporal-AI/dataset/libero \
    ASSETS_ROOT=/workspace/openpi-jax010-hcu/assets \
    bash /workspace/openpi-jax010-hcu/datadown.sh

    # 启动八卡训练(全局 bs384,30000 步;BATCH_SIZE 是单进程 JAX 的全局 batch,不乘 8)
    docker exec -it openpi-jax010-hcu env \
      OPENPI_REPO_ROOT=/workspace/openpi-jax010-hcu \
      OPENPI_SOURCE_ROOT=/workspace/openpi \
      BATCH_SIZE=384 FSDP_DEVICES=8 STEPS=30000 \
      bash /workspace/openpi-jax010-hcu/start_openpi.sh
    ```

    启动脚本会自动完成"源码定位 + patch 应用 + 训练启动",并把源码路径、patch SHA256、运行时配置、训练日志与状态写入运行输出目录下的 `run-metadata/`。

默认配置为八卡 FSDP:全局 BS384、30000 步。首次运行需编译(约 10 分钟),保留 `~/.cache/jax` 后再次运行约 25 秒;吞吐测试用默认 `--log-interval=100`(`--log-interval=1` 有每步 wandb 开销)。

## 模型列表

### 全参 微调

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
      <td><a href="https://github.com/Physical-Intelligence/openpi">pi05_base</a></td>
      <td>OpenPI-JAX</td>
      <td>BF16</td>
      <td><a href="https://zzefile.scnet.cn:65011/efile/s/d/cWlhbnlqMQ==/c138b78040d3e420">openpi_jax010_dtk26042_v1</a></td>
      <td>8(gfx936)</td>
      <td>-</td>
      <td align="center">start_openpi.sh</td>
    </tr>
  </tbody>
</table>
