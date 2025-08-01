### Jupyter Lab

由于连接gpu是通过master进行的，所以需要进行端口转发。

首先在gpu上安装jupyterlab并运行，以接口为4190为例

```bash
jupyter lab --no-browser --port=4190 --ip=0.0.0.0
或使用nohup
nohup jupyter lab --no-browser --port=4190 --ip=0.0.0.0 > jupyterlab.log 2>&1 &
```

之后在在本地电脑打开终端，连接master进行端口转发

```bash
ssh -L 4190:10.0.0.152:4190 liuzixuan@211.81.48.139
```

上述过程需要确定防火墙是否开放端口

可以将conda环境导入到jupytelab

```bash
python -m ipykernel install --user --name <conda env name> --display-name "<jupyter display name>"
```

需要将<conda env name>和<jupyter display name>进行替换
