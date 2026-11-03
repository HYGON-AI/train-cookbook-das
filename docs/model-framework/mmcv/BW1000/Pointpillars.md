# Pointpillars

## 模型简介

PointPillars 是一种基于激光雷达点云的 3D 目标检测模型，将点云划分为垂直柱状体（pillar）并通过 PointNet 提取特征，再转换为伪图像后使用 2D 卷积网络完成端到端 3D 目标检测。


## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">精度</th>
      <th colspan="2" style="text-align:center">环境版本</th>
      <th colspan="3" style="text-align:center">推荐训练参数</th>
      <th rowspan="2">示例脚本</th>
    </tr>
    <tr>
      <th>torch</th>
      <th>mmcv</th>
      <th>Batch Size</th>
      <th>Global Batch Size</th>
      <th>Epoch</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Pointpillars</td>
      <td>8</td>
      <td>FP32</td>
      <td>2.7.1</td>
      <td>1.6.1</td>
      <td>4</td>
      <td>32</td>
      <td>24</td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/blob/bw1101_hygon/models/PointPillars/PointPillars/mmdetection3d/start_pointpillars.sh">✅</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- PointPillars 原生支持 BF16，在 HCU 上运行稳定
- 构建 PointPillars 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

