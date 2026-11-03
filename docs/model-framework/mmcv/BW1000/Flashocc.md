# Flashocc

## 模型简介

FlashOCC 是面向自动驾驶的轻量级 3D 占据网格（occupancy）预测模型，通过显式深度监督与特征融合，以较低计算开销实现多相机环视场景下的占据感知。


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
      <td>Flashocc</td>
      <td>8</td>
      <td>FP32</td>
      <td>2.7.1</td>
      <td>1.6.1</td>
      <td>4</td>
      <td>32</td>
      <td>24</td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/blob/bw1101_hygon/models/FlashOCC/FlashOCC/start_flashocc.sh">✅</a></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- FlashOCC 原生支持 BF16，在 HCU 上运行稳定
- 构建 FlashOcc 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

