# Pointpillars

## 模型简介

PointPillars 是一种基于激光雷达点云的 3D 目标检测模型，将点云划分为垂直柱状体（pillar）并通过 PointNet 提取特征，再转换为伪图像后使用 2D 卷积网络完成端到端 3D 目标检测。


## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">测试卡数</th>
      <th rowspan="2">精度</th>
      <th colspan="3" style="text-align:center">训练参数</th>
      <th colspan="3" style="text-align:center">模型精度</th>
      <th rowspan="2">吞吐量(imgs/sec/gpu)</th>
      <th rowspan="2">日志</th>
      <th rowspan="2">环境构建</th>
    </tr>
    <tr>
      <th>batch size</th>
      <th>global batch size</th>
      <th>epoch</th>
      <th>NDS</th>
      <th>mAP</th>
      <th>Final Loss</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Pointpillars</td>
      <td>8</td>
      <td>FP32</td>
      <td>4</td>
      <td>32</td>
      <td>24</td>
      <td>0.5097</td>
      <td>0.3727</td>
      <td>0.3491</td>
      <td>11.05</td>
      <td><a href="./logs/bw1000_pointpillars_8card_bs4_24e_fp32.log">log</a></td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/models/PointPillars">link</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- PointPillars 原生支持 BF16，在 HCU 上运行稳定
- 构建 PointPillars 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

