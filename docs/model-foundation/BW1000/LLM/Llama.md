# Llama2/3

## 模型简介

Llama2 和 Llama3 是 Meta 开源的大语言模型，均为dense模型，支持 7B ~ 405B 多种参数规模。

## 推荐镜像
docker pull harbor.sourcefind.cn:5443/dcu/admin/base/custom:pytorch2.9.0-ubuntu22.04-dtk26.04-py3.10_te2.10

## 模型列表

<table>
  <thead>
    <tr>
      <th rowspan="2">模型</th>
      <th rowspan="2">精度</th>
      <th rowspan="2">torch版本</th>
      <th rowspan="2">TE版本</th>
      <th rowspan="2">推荐卡数</th>
      <th rowspan="2">序列长度</th>
      <th rowspan="2">示例脚本</th>
      <th rowspan="2">性能参考</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://www.modelscope.cn/models/LLM-Research/llama-2-7b">llama2-7B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/llama2">✅</a></td>
      <td align="center"></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/shakechen/Llama-2-13b">llama2-13B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/llama2">✅</a></td>
      <td align="center"></td>
    </tr>
    <tr>
      <td><a href="https://huggingface.co/meta-llama/Llama-2-70b">llama2-70B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>64</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/llama2">✅</a></td>
      <td align="center">tgs=512</td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/LLM-Research/Meta-Llama-3-8B">llama3-8B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>8</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/llama3">✅</a></td>
      <td align="center"></td>
    </tr>
    <tr>
      <td><a href="https://www.modelscope.cn/models/LLM-Research/Meta-Llama-3-70B">llama3-70B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>64</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/llama3">✅</a></td>
      <td align="center"></td>
    </tr>
        <tr>
      <td><a href="https://www.modelscope.cn/models/LLM-Research/Meta-Llama-3.1-405B">llama3-405B</a></td>
      <td>BF16</td><td>2.9</td><td>2.10</td>
      <td>512</td>
      <td><=4096</td>
      <td align="center"><a href="http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/tree/core_v0.18.2/examples/llama3">✅</a></td>
      <td align="center"></td>
    </tr>
  </tbody>
</table>

## HCU 适配注意

- Llama2 和 Llama3 原生支持 bf16，在 HCU 上运行稳定
- Llama2 和 Llama3 均为dense模型，没有moe结构
