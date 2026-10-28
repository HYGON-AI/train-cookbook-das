# Bevformer

## 模型简介

BEVFormer 是基于 Transformer 的鸟瞰视角（BEV）3D 目标检测模型，通过空间注意力与时间注意力聚合多视角相机特征，面向自动驾驶场景进行端到端 3D 目标检测。


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
      <td>Bevformer</td>
      <td>8</td>
      <td>FP32</td>
      <td>2</td>
      <td>16</td>
      <td>24</td>
      <td>0.503</td>
      <td>0.4141</td>
      <td>3.36</td>
      <td>1.02</td>
      <td><a href="./logs/bw1100_bevformer_8card_bs2_24e_fp32.log">log</a></td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/models/BEVFormer">link</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- BEVFormer 原生支持 BF16，在 HCU 上运行稳定
- 构建 BEVFormer 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

