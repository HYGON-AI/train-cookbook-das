# Bevfusion

## 模型简介

BEVFusion 是一种多模态 3D 目标检测模型，融合相机与激光雷达点云特征，在统一的鸟瞰视角（BEV）表示下进行端到端检测，兼顾几何感知与语义理解。


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
      <td>Bevfusion</td>
      <td>8</td>
      <td>FP16</td>
      <td>4</td>
      <td>32</td>
      <td>6</td>
      <td>0.5987</td>
      <td>0.5813</td>
      <td>1.0809</td>
      <td>1.8482</td>
      <td><a href="./logs/BW1100_bevfusion_8card_bs4_6e_fp16.log">log</a></td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/models/BEVFusion">link</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- BEVFusion 原生支持 BF16，在 HCU 上运行稳定
- 构建 BEVFusion 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

