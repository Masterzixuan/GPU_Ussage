### Slurm

所有涉及到GPU、多核的作业都必须通过Slurm提交作业，否则系统容易崩溃～！

可以自己查阅Slurm使用教程，此处仅有简单的使用教程及示例

- 创建一个sh文件用于提交作业

  ```bash
  nano test.sh
  ```

- 编辑sh文件

  ```sh
  #!/bin/bash
  #SBATCH --job-name=nn_test         # 作业名称
  #SBATCH --partition=batch            # 分区名称（根据你的slurm.conf调整）
  #SBATCH --account=tju            # 账户名称（使用tju账户）
  #SBATCH --qos=normal                # QoS名称（使用normal QoS）
  #SBATCH --nodes=1                  # 请求1个节点
  #SBATCH --ntasks=1                 # 请求1个任务
  #SBATCH --cpus-per-task=16          # 每个任务使用16个CPU核心
  #SBATCH --mem=8G                   # 请求8GB内存
  #SBATCH --gres=gpu:1               # 请求1个GPU
  #SBATCH --time=01:00:00            # 作业最大运行时间1小时
  #SBATCH --output=test_%j.out    # 输出文件名（%j为作业ID）
  #SBATCH --error=test_%j.err     # 错误文件名
  
  # 初始化 Conda 环境
  source /usr/local/anaconda3/etc/profile.d/conda.sh  # 使用你的base环境路径
  conda activate torch28  #在此激活你要使用的conda环境
  
  # 设置 CUDA 环境变量
  export PATH=/usr/local/cuda-12.8/bin:$PATH
  export LD_LIBRARY_PATH=/usr/local/cuda-12.8/lib64:$LD_LIBRARY_PATH
  
  # 打印环境信息
  echo "Job ID: $SLURM_JOB_ID"
  echo "Node: $SLURMD_NODENAME"
  echo "Partition: $SLURM_JOB_PARTITION"
  echo "Account: $SLURM_JOB_ACCOUNT"
  echo "QoS: $SLURM_JOB_QOS"
  echo "Python Path: $(which python3)"
  echo "CUDA Version: $(nvcc --version)"
  echo "PyTorch CUDA: $(python3 -c 'import torch; print(torch.version.cuda)')"
  echo "GPU Available: $(python3 -c 'import torch; print(torch.cuda.is_available())')"
  echo "GPU Name: $(python3 -c 'import torch; print(torch.cuda.get_device_name(0))')"
  echo "Start Time: $(date)"
  
  # 运行 Python 脚本
  # 在此修改你要运行的脚本
  python3 test.py
  
  # 退出 Conda 环境
  conda deactivate
  
  echo "Job finished at: $(date)"
  ```

- 提交、查看、取消作业

  ```bash
  sinfo # 查看当前状态
  sbatch test.sh # 提交作业
  squeue # 查看个人作业状态
  scancel <jobid> # 取消<jobid>的作业
  ```

### 
