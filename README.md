# GPU集群使用

目前主节点为master，具有固定IP，需在校园网环境下连接  
IP:`211.81.48.139`

连接gpu节点需要以master为跳板机，先ssh到master后在ssh gpu
```
ssh username@211.81.48.139
ssh gpu
```
**注意：所有GPU作业都需通过Slurm提交，通过节点连接的python和jupyter都只允许进行简单的单核cpu作业（如绘图、数据预处理……）！！！不允许通过jupyterlab及python运行多核、大内存占用、GPU等作业！！！**

# 存储状态
/dev/nvme2n1p2             1.8T  7.2G  1.7T   1% /home  
/dev/nvme0n1p1             7.0T   50G  7.0T   1% /Data  
/dev/nvme1n1p1             7.0T   50G  7.0T   1% /home/Data  
目前可用的有三块硬盘，分别挂载在不同的路径下
## 1 M.2 NVME SSD 2TB
这个硬盘目前挂载在`/home`路径下，仅用于存储用户的文件夹以及重要代码，模型checkpoint

## 2 U.2 NVME SSD 7TB
这个硬盘挂载在/Data，用户可在该路径下创建文件夹存储训练数据

## 3 U.2 NVME SSD 7TB
这个硬盘挂载在/home/Data，用户可在该路径下创建文件夹存储训练数据

# 共享路径
为了方便数据传输，我们将主节点的`/home`路径共享到校园网内的服务器上，用户可以通过`/mnt/test_share`访问自己的文件夹