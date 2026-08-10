# FAQ

## 基础问题
### 如何使用HCU？
在HCU上跑一个AI模型模型，请参考[快速开始](http://42.228.13.241:10068/dcutoolkit/deeplearing/dcu_megatron/-/blob/core_v0.18.2/docs/getting-started.md)。

### 如何多节点训练？
#### 配置容器跨节点免密
1. 进入容器，启动端口，PORT替换为端口号。
   `/usr/sbin/sshd -p PORT` 
2.  生成 SSH 密钥对
   `ssh-keygen -ted25519`
   
3. 分发公钥
   在每个容器的`/root/.ssh/authorized_keys`文件中添加所有节点的公钥, 保证所有容器内的authorized_keys文件内容一致。
4. 验证配置
   在任一节点的容器内执行，确认无需密码即可登录其他节点。host_ip替换为其他节点的IP，PORT替换为端口号。
   `ssh host_ip -p PORT`
#### 在mpirun中添加免密端口
在启动脚本的mpirun命令中添加 ` --mca plm_rsh_args "-p PORT"`
示例：
``` bash
mpirun -np ${GPUS}  --hostfile ${HOSTFILE} \
                    --allow-run-as-root \
                    --bind-to none \
                    --mca plm_rsh_no_tree_spawn 1 \
                    --mca plm_rsh_args "-p PORT" \
                    bash -c "
                    source ${DTK_ENV} && \
                    source ${NCCL_ENV} && \
                    bash train_qwen3_30B_A3B.sh \
                    ${HOST} \
                    ${PORT} \
                    --data_path=$DATA_PATH \
                    --tokenizer_path=$TOKENIZER_MODEL_PATH \
                    --checkpoint_path=$CHECKPOINT_PATH \
                    --launch_with_binding=${LAUNCH_WITH_BINDING} \
                    --profiling=$profiling" 2>&1|tee log-$((${GPUS} / 8))nodes-`date +%F-%H%M`.log 
```
#### 注意事项
多节点训练时，要保证各节点的IB网卡和socket设置配置正确。NCCL_IB_HCA要写参与训练节点均可使用的IB网卡，GLOO_SOCKET_IFNAME指定Gloo后端使用的网络接口，可针对不同节点个性化设置。
示例：
```bash
if [[ "$NODE_HOSTNAME" == *"ip1"* ]]; then
    # 节点1的配置
    export GLOO_SOCKET_IFNAME=NAME1 
elif [[ "$NODE_HOSTNAME" == *"ip2"* ]]; then
    # 节点2的配置
    export GLOO_SOCKET_IFNAME=NAME2
else
    # 默认配置
    export GLOO_SOCKET_IFNAME=NAME3
fi
```

### HCU-Megatron和Megatron-LM有什么区别？
HCU-Megatron是基于海光 HCU，将 NVIDIA 的 Megatron-LM移植并适配到海光 HCU 平台。与Megatron-LM的主要区别：
- **编程模型**: 使用 HIP（Heterogeneous-compute Interface for Portability），兼容 CUDA API
- **软件栈**: DTK 替代 CUDA Toolkit
- **生态**: 部分框架需要适配，主流框架（PyTorch、vLLM等）已支持
- **优化重点**：算子适配与融合、通信优化、架构兼容

### HCU-Megatron的性能如何？
HCU-Megatron 的性能表现通常可以达到同级别 NVIDIA GPU 的 **100% - 150%**。
BW1000对标Nvidia A100，BW1100对标Nvidia H20。

### HCU-Megatron优势场景是那些？
HCU-Megatron 的优势场景主要包括常见的dense模型,如Llama2（7B/13B/70B），Qwen3（8B/14B）等。