# 简介
optimization文件夹包含针对多种模型的调优建议。
# 大模型训练常见调优方式
## 1. 通用优化方式
本节适用于所有模型架构（Dense、MoE、VL）的基础优化手段。
### 1.1 Flash attn（FA）

FA属于通用的优化手段, 可以加快self attn的计算, 减少显存的占用。

开启方式:

```python
--use-flash-attn
```

### 1.2 通信与计算重叠（常规Overlap）

```Python
--overlap-param-gather # 参数收集与前一层的计算重叠（ZeRO/FSDP场景）
--overlap-grad-reduce  # 梯度规约与后一层的计算重叠
```
## 2. 精度换性能优化
⚠️ 本节适用于对精度要求不高的场景，通过降低精度换取性能提升。
### 2.1 半精度梯度规约
```python
--grad-reduce-in-bf16
```
### 2.2 半精度梯度与参数存储
```python
--use-precision-aware-optimizer
--main-grads-dtype bf16     #可选值 fp32 / bf16
--main-params-dtype fp16    #可选值 fp32 / fp16
```
### 2.3 半精度优化器状态
```python
--use-precision-aware-optimizer    
--exp-avg-dtype bf16         #可选值 fp32 / fp16 / bf16 / fp8
--exp-avg-sq-dtype bf16      #可选值 fp32 / fp16 / bf16 / fp8
```
### 2.4 FP8 训练
```python
# 启动参数
--fp8-format hybrid          
--fp8-recipe tensorwise      # tensorwise 或 allreduce
--fp8-param-gather           # 参数收集使用 FP8
```
### 2.5 交叉熵融合（Cross-Entropy Fusion）
```python
--cross-entropy-loss-fusion      # 启用融合 CE Loss
--cross-entropy-fusion-impl te   # 使用 TransformerEngine 实现
```
## 3. 显存不足优化
适用场景：模型规模超过单卡显存容量，或 GPU 数量受限无法充分切分。

### 3.1 参数副本复用
```python
--use-optimizer-feature   # 启用优化器特征复用
--reuse-fp32-param        # FP32 参数副本复用
```
### 3.2 Swap Attention（注意力张量交换）
将 Attention 层的中间激活值交换到 CPU 内存，需要时再换回 GPU。
```python
必选:
--swap-attention
可选:
--swap-modules input_layernorm,self_attention,post_attention_norm
--specify-layers 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15
```
### 3.3 Optimizer Offload（优化器状态卸载）
```python
--optimizer-cpu-offload
--optimizer-offload-fraction 1.0
--use-torch-optimizer-for-cpu-offload
--use-precision-aware-optimizer
```
### 3.4 Cpu Offload（参数卸载）
将模型参数卸载到 CPU 内存，需要时再加载到 GPU。

参考文档：[cpu offload测试](https://kcnm6g5dkw5p.feishu.cn/wiki/OHQKwY5Wui7oU1kmmIbcySDTnYf)

### 3.5 Activation Offload（激活值卸载）
将前向计算的激活值卸载到 CPU 内存，反向时再加载回来。
```python
--fine-grained-activation-offloading   # 细粒度激活卸载
--offload-modules core_attn attn_proj qkv_linear   # 指定卸载模块
```

## 4. 显存充裕优化
适用场景：固定切分超参无法更改，但显存较为充裕，可以用显存换取计算/通信效率。

### 4.1 关闭序列并行（Sequence Parallelism）
关闭sp, 减少sp切分导致的ag和rs通信
```python
--sequence-parallel    
# 但是收益可能为负
```
### 4.2 开启 Virtual Pipeline
通过 VP 减少 Pipeline Parallelism 的空泡（Bubble）占比。

示例如下：
```Python
--num-layers-per-virtual-pipeline-stage  # 每个 VP 阶段的层数

--pipeline-model-parallel-layout "Ettttt|(ttttt|)*14tttttL"
# E: Embedding, t: transformer layer, L: Loss
# 该布局表示将模型切分为多个 VP 阶段，每个阶段含 5 个 Transformer 层
```

### 4.3 Flux TP Overlap（Tensor Parallelism 通信重叠）
使用 Flux 实现方案，利用额外显存换取 TP 通信与计算的 Overlap。

示例如下：
```Python
--parallel-linear-impl flux   # 使用 Flux 的并行线性层实现
```

### 4.4 1F1B 流水线优化
将PP的反向传播中的 W-Grad 和 Y-Grad 拆分为两个独立的计算阶段，实现更细粒度的流水调度。

详细参考: http://42\.228\.13\.241:10068/dcutoolkit/deeplearing/dcu\_megatron/\-/blob/core\_v0\.18\.2/docs/features/pipeline\-parallel\.md

注意事项：

该优化可能依赖 NCCL P2P 通信，若卡住可尝试调整以下环境变量：
```Python
#卡住时可能要将rccl的p2p相关参数删掉
export NCCL_NCHANNELS_PER_PEER=2
export NCCL_MIN_P2P_NCHANNELS=32
export NCCL_MAX_P2P_NCHANNELS=32

--delay-1f1b-cooldown-wgrad-compute
--delay-wgrad-compute # 使用delay-1f1b-cooldown-wgrad-compute时自动开启该参数，可去掉
```
## 5. Dense 模型优化
适用场景：适用于标准 Transformer Dense 架构。

### 5.1 Flux 优化的 TP-Comm Overlap
```python
--tp-comm-overlap          
```
## 6. MoE 模型优化
适用场景：适用于 Mixture of Experts（混合专家）架构。
### 基础参数配置
```python
--moe-ffn-hidden-size 8192          # MoE FFN 隐藏层维度
--num-experts 16                    # 专家数量
--moe-aux-loss-coeff 0.001          # 辅助损失系数（用于负载均衡）
--moe-router-dtype fp32             # 路由器计算精度，推荐 FP32 保证路由稳定性
```

### 6.1 MoE 层切分策略
```Python
--expert-model-parallel-size 8
--expert-tensor-parallel-size 1
```
### 6.2 通信后端
```Python
--moe-token-dispatcher-type alltoall # flex
--moe-flex-dispatcher-backend hybridep # deepep
```
### 6.3 量化通信

```Python
#必选参数
--use-quantize-comm
#可选参数
--quant-comm-bits 4          # 量化精度, 可取4/8，分别将数据量化为int4/int8，缺省值为8；
--quant-group-size 32        # 数据被分成大小为quant-group-size的组，每组应用特定的量化策略，有助于提高量化效果或保持模型性能。quant-comm-bits为4时，quant-group-size可取16或32，默认为32。quant-comm-bits为8时，quant-group-size可取64或128，默认为128。

```
### 6.4 融合gemm
将多个专家的独立矩阵乘融合为单个大矩阵乘
```Python
export NVTE_USE_HIPBLASLT_GROUPEDGEMM=1
--moe-grouped-gemm
```
### 6.5 融合算子
将多个专家的独立矩阵乘融合为单个大矩阵乘
```Python
--moe-permute-fusion      # Token Permute/Unpermute 与 GEMM 融合
--moe-router-fusion       # Router Softmax + Top-K 融合
```
### 6.6 MoE 负载均衡

```Python
--moe-router-force-load-balancing   # 强制路由器负载均衡
```