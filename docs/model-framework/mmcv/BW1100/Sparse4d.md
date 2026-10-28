# Sparse4d

## 模型简介

Sparse4D 是一种基于稀疏查询的端到端 4D 感知模型，通过时空建模在鸟瞰视角（BEV）中关联多帧相机特征，用于自动驾驶场景下的 3D 目标检测与跟踪。


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
      <td>Sparse4d</td>
      <td>8</td>
      <td>FP16</td>
      <td>8</td>
      <td>64</td>
      <td>100</td>
      <td>0.5692</td>
      <td>0.4659</td>
      <td>11.4795</td>
      <td>9.939</td>
      <td><a href="./logs/bw1100_sparse4d_8card_bs8_100e_fp16.log">log</a></td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/models/Sparse4D">link</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Sparse4D 原生支持 BF16，在 HCU 上运行稳定
- 构建 Sparse4D 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

