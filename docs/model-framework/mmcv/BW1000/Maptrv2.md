# Maptrv2

## 模型简介

MapTRv2 是一种端到端的高精地图构建模型，基于统一的 Transformer 感知框架，在鸟瞰视角（BEV）中并行检测车道线、人行横道和道路边界等矢量化地图元素。


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
      <td>Maptrv2</td>
      <td>8</td>
      <td>BF16</td>
      <td>2.7.1</td>
      <td>1.6.1</td>
      <td>12</td>
      <td>96</td>
      <td>24</td>
      <td><a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/blob/bw1101_hygon/models/MapTRv2/start_maptrv2.sh">✅</a></td>
    </tr>
  </tbody>
</table>


## HCU 适配注意

- MapTRv2 原生支持 BF16，在 HCU 上运行稳定
- 构建 MapTRv2 镜像环境前，请先完成其依赖的上层镜像构建，具体参考<a href="https://developer.sourcefind.cn/codes/ts-models-opt/training/autonomous-driving-models/-/tree/bw1101_hygon/">镜像构建说明</a>

