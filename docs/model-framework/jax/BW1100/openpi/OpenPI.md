# OpenPI (π05)

## 模型简介

OpenPI 是 Physical Intelligence 开源的视觉-语言-动作(VLA)模型训练框架,本方案基于其中的 π05 模型,采用 JAX 实现,在 HCU 上完成 LIBERO 具身任务的微调训练。交付形式为**运行环境镜像 + 官方 OpenPI 源码 + 独立优化 patch + 启动脚本**,优化通过 `patches/model_optimizations.patch` 提供,镜像内已安装优化后的 JAX/XLA、FA、BLAS 及专用算子。

## 使用示例

1. 下载并导入优化镜像(下载支持断点续传,压缩包可直接 `docker load` 导入):

    ```bash
    curl -f -C - -o openpi-jax-optimized_20261021.tar.gz https://ksefile.hpccube.com:65241/efile/s/d/c2NubXFneDI4ZQ==/e0933fc7d2b52c9f
    docker load -i openpi-jax-optimized_20261021.tar.gz
    ```

2. 创建容器并挂载数据和权重(将 `/实际路径/...` 替换为宿主机对应目录,镜像名使用 `docker load` 输出的 Loaded image 名称):

    ```bash
    docker run -it --name openpi-jax010-hcu --network=host \
      --device=/dev/kfd --device=/dev/dri --group-add video \
      --ipc=host \
      -v /opt/hyhal:/opt/hyhal:ro \
      -v /实际路径/libero:/embodied/model/Spatialtemporal-AI/dataset/libero:ro \
      -v /实际路径/openpi-assets:/embodied/model/Spatialtemporal-AI/openpi-assets:ro \
      -v /实际路径/训练输出:/home/openpi-runs \
      镜像名:标签 /bin/bash
    ```

3. 容器内 clone 本仓库,检查外部资源后启动训练:

    ```bash
    git clone https://developer.sourcefind.cn/codes/ts-models-opt/training/embodied-ai.git /home/code/embodied-ai
    cd /home/code/embodied-ai/openpi-jax010-hcu
    bash datadown.sh                # 仅检查外部资源路径,不下载、不占 GPU
    bash start_openpi.sh --help
    bash start_openpi.sh            # 确认八张可见卡可用后执行
    ```

默认采用最优八卡 DDP 配置:全局 BS256、每卡 BS32,启动脚本自动识别可见 GPU 及其 PCI/NUMA 拓扑并分配进程,无需配置节点名、profile 或设备编号。默认运行 3000 步(前 10 步预热、后 2990 步计时),该配置为**性能复现配置**(EMA、checkpoint 保存、逐步范数统计和裁剪范数计算均已关闭),正式长训需按任务恢复相应设置。

## 模型列表

### 全参 微调(性能复现)

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
      <td>BF16(FP32 master)</td>
      <td><a href="https://ksefile.hpccube.com:65241/efile/s/d/c2NubXFneDI4ZQ==/e0933fc7d2b52c9f">openpi-jax-optimized_20261021</a></td>
      <td>8(gfx938/64CU)</td>
      <td>-</td>
      <td align="center"><a href="https://github.com/Physical-Intelligence/openpi/blob/master/scripts/train.py">link</a></td>
    </tr>
  </tbody>
</table>
