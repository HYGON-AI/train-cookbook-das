# 模型特性扩展

hcu-megatron 通过替换 Megatron 的函数或类，为已有模型引入新特性，或扩展支持更多 HuggingFace 模型架构。

- [MHC 超连接](#mhc-超连接)
- [Megatron-Bridge](#megatron-bridge)

## MHC 超连接

hcu-megatron 0.17.0 新增 MHC（Hyper Connections，多残差流）实现，提供 torch 原生和 tile_kernel 两种方式：

- **torch 原生实现**：支持重计算，兼容性好
- **tile_kernel 实现**：性能更优，但不支持重计算

### torch 原生实现

```bash
--enable-hyper-connections
```

### tile_kernel 实现

```bash
--enable-hyper-connections
--mhc-use-tilekernels
--mhc-fuse-h-post-compute
--mhc-tau 1.0
--mhc-log-amax-per-step 20
```

使用 tile_kernel 前需完成以下配置：

```bash
# 1. 获取 hcu 版本的 tile-kernels 并安装；或将代码放到指定目录并手动设置
# 假设 tile_kernels 目录在 Megatron-LM/megatron 下
export PYTHONPATH=/mnt/hcu_megatron/Megatron-LM/megatron/:$PYTHONPATH

# 2. 查找环境的 python 目录，设置 z3/lib 路径
export LD_LIBRARY_PATH="/usr/local/lib/python3.11/site-packages/z3/lib:$LD_LIBRARY_PATH"
```

### 开启 MHC 重计算

仅 torch 原生实现支持重计算：

```bash
--recompute-granularity selective
--recompute-modules layernorm core_attn mhc
```

### 其他常用参数

```bash
--num-residual-streams 4               # 残差流数量（论文中的 n），默认 4
--mhc-init-gating-factor 0.01          # Gating Factor 初值（论文中的 alpha）
--mhc-sinkhorn-iterations 1            # Sinkhorn-Knopp 迭代次数，需 ≤ 10
--mhc-recompute-layer-num 1            # 每个 MHC 重计算 block 的层数
--mhc-expand-emb                       # 是否扩展 embedding 维度
--mhc-lite                             # 使用 lite 版本
--use-vwn                              # 使用 vwn
--mhc-hres-vwnstyle                    # 使用 vwn 风格的 h_res
--use-mhc-svd                          # 使用 SVD
--mhc-fix-muons                        # 修复 muons
--mhc-fuse-aggregate-compute           # 融合 aggregate 计算
--mhc-init-hpre-use-module-layer       # 使用模块级 layer index 初始化 h_pre
```

### 注意事项

1. torch 原生实现支持重计算，tile_kernel 实现不支持重计算
2. `--mhc-sinkhorn-iterations` 参数需设置为 ≤ 10

## Megatron-Bridge

基于 Megatron-Bridge 可通过 Megatron 直接训练更多 HuggingFace 模型架构，无需手动转换模型配置。

### 使用方式

```bash
--use-bridge
--bridge-hf-model ${TOKENIZER_MODEL_PATH}
--load-weights                        # 可选，加载 HF 预训练权重
```

### 工作原理

Bridge 通过读取 HF `config.json` 中的 `architectures` 字段自动分发到对应的 Bridge 实现（如 `Qwen3_5ForConditionalGeneration` → `Qwen35VLBridge`），将 HF 模型配置转换为 Megatron 格式的 `ModelProvider`，最终构建 Megatron 分布式模型。

调用链示意（以 qwen3.5vl 为例）：

```
setup_model_and_optimizer()
  │
  ├─ AutoBridge.from_hf_pretrained(args.bridge_hf_model)
  │    │  读取 config.json → architectures: ["Qwen3_5VLForConditionalGeneration"]
  │    │  校验后缀为 "ForCausalLM" / "ForConditionalGeneration"
  │    └─ 返回 AutoBridge(hf_pretrained)
  │
  ├─ bridge.to_megatron_provider(load_weights=True, hf_path=...)
  │    │  dispatch 到已注册的 Qwen35VLBridge
  │    │  → Qwen35VLModelProvider(TransformerConfig 子类)
  │    │  → 注入 vision_config / mrope / token_ids
  │    └─ 用 CLI args 覆盖分布式并行参数（TP/PP/CP）后 finalize()
  │
  └─ provider.provide_distributed_model(wrap_with_ddp, ddp_config)
       └─ 根据并行参数切分并包裹模型 → Qwen3VLModel（Megatron 格式）
```
