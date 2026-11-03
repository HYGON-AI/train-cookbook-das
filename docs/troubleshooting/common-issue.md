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
举例：有 eth0 高速网卡, eth1 已 donw 的网卡, eth2 管理网卡等

最终参数：
```shell
export GLOO_SOCKET_IFNAME=eth0
export NCCL_SOCKET_IFNAME=eth0
```
      
### 模型路径
模型下载：已适配模型可在对应md文件中，通过点击模型名称跳转至模型所在页面进行下载。

## 训练问题

### 训练出现OOM（Out of Memory）

1. 检查有没有人复用节点
2. 减少序列长度`--seq_length`或者增加切分`--tensor-model-parallel-size`
3. 开启激活重算
4. 使用精度优化器

### 训练速度异常慢

1. 检查有没有人复用节点
2. 多节点训练时检查多机网卡是否配置正确
3. hcu频率是否一致`hy-smi -c`