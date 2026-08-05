# 常见问题

## 环境相关

### IB网卡

配置的网卡需要满足：
1.ibstat查询状态为Active
2.未用于存储

举例环境网卡状态：
1.存储网卡：mlx5_0,mlx5_1
2.状态Down网卡：mlx5_6,mlx5_7
3.状态Active网卡：mlx5_0,mlx5_1,mlx5_2,mlx5_3,mlx5_4,mlx5_5,mlx5_8,mlx5_9

有效设备：mlx5_2,mlx5_3,mlx5_4,mlx5_5,mlx5_8,mlx5_9

最终参数：
export NCCL_IB_HCA=mlx5_2:1,mlx5_3:1,mlx5_4:1,mlx5_5:1,mlx5_8:1,mlx5_9:1

### socket配置
1.ifconfig -a 在容器内查看所有网卡
2.找到ip对应的网卡名称

举例：
``` python
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:b8ff:fe9b:7d7e  prefixlen 64  scopeid 0x20<link>
        ether 02:42:b8:9b:7d:7e  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7  bytes 690 (690.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp113s0f0np0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9216
        inet 12.12.12.61  netmask 255.255.0.0  broadcast 12.12.255.255
        inet6 fe80::5e25:73ff:fea1:27e2  prefixlen 64  scopeid 0x20<link>
        ether 5c:25:73:a1:27:e2  txqueuelen 1000  (Ethernet)
        RX packets 80063120  bytes 481682520186 (448.6 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 76079361  bytes 370901307661 (345.4 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp113s0f1np1: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 5c:25:73:a1:27:e3  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp225s0f0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.16.1.61  netmask 255.255.255.0  broadcast 10.16.1.255
        inet6 fe80::8261:5fff:fe26:40b7  prefixlen 64  scopeid 0x20<link>
        ether 80:61:5f:26:40:b7  txqueuelen 1000  (Ethernet)
        RX packets 10214193  bytes 9736471256 (9.0 GiB)
        RX errors 0  dropped 1029  overruns 1029  frame 0
        TX packets 4970867  bytes 2475289418 (2.3 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device memory 0x71180000-711fffff  
```
最终参数：
export GLOO_SOCKET_IFNAME=enp225s0f0

### 数据集
LLM模型所用数据集

小规模用Oscar，约1GB

中等规模用c4，约300GB

更大规模用RedPajama\-Data\-1T

数据集下载 (Oscar数据集举例)：
    `modelscope download --dataset kanliu/oscar-en-10k-megatron oscar-en-10k.jsonl --local_dir ./oscar-en-10k`

处理数据集
    ```bash
    python Megatron-LM/tools/preprocess_data.py \
        --tokenizer-type HuggingFaceTokenizer \
        --tokenizer-model ./Qwen3-8B \
        --input ./oscar-en-10k/oscar-en-10k.jsonl \
        --output-prefix ./oscar-en-10k/oscar-en-10k-qwen3 \
        --append-eod \
        --workers 16
    ```
    处理完成后会分别保存为.bin和.idx文件

在启动脚本（run.sh）中配置数据集路径。
举例（Qwen3模型）：
    `DATA_PATH="/workspace/qwen3/mmap_qwen3_datasets_text_document" ` 

                    
### 模型路径
模型下载：
1.已适配模型可在对应md文件中，通过点击模型名称跳转至模型所在页面进行下载。
2.   可通过命令直接下载，示例如下：
     `modelscope download --model Qwen/Qwen3-8B --local_dir ./Qwen3-8B`

路径配置：
在启动脚本（run.sh）中配置模型路径。

举例（Qwen3模型）：
    `TOKENIZER_MODEL_PATH="/workspace/model_config/qwen3/qwen3-30b-a3b"                                                  
` 
### 训练出现OOM（Out of Memory）

**解决方案（按优先级）：**

1. 减小 `--global-batch-size`和--micro batch size
2. 降低 `--seq-length`
3. 增加 `--tensor-parallel-size`
4. 使用FA`--use-flash-attn`
5. 开启激活重算
   `--recompute-granularity selective  `
6. 使用精度感知优化器
    ```bash
     --use-precision-aware-optimizer 
     --main-grads-dtype bf16
     --main-params-dtype fp16
     --exp-avg-dtype bf16
     --exp-avg-sq-dtype bf16`
### 训练速度异常慢

```bash
# 1. 确认数据类型
# 应使用 bf16，而非 fp32

# 2. 检查 HCU 利用率
hy-smi

# 3. 确认 tensor-parallel 配置合理

# 4. 检查是否有 CPU 瓶颈
htop
```