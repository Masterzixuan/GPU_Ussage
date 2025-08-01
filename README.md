# GPU集群使用

目前主节点为master，具有固定IP，需在校园网环境下连接  
IP：**211.81.48.139**

连接gpu节点需要以master为跳板机，先ssh到master后在ssh gpu

**注意：所有GPU作业都需通过Slurm提交，通过节点连接的python和jupyter都只允许进行简单的单核cpu作业（如绘图、数据预处理……）！！！不允许通过jupyterlab及python运行多核、大内存占用、GPU等作业！！！**
