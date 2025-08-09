### 远程访问（Pycharm）

本地电脑通过跳板机（master）连接到GPU服务器（GPU），需要免密连接，才能直接访问GPU服务器的文件

1、在本地生成SSH密钥对，按回车接受默认文件路径（~/.ssh/id_rsa 和 ~/.ssh/id_rsa.pub）(在本地命令行执行)

```bash
ssh-keygen
```

2、将公钥复制到 master 和 GPU 服务器(在本地命令行执行)

```bash
ssh-copy-id liuzixuan@211.81.48.139 # copy to master
ssh-copy-id -o ProxyJump=liuzixuan@211.81.48.139 liuzixuan@gpu # copy to GPU server
```

3、编辑本地SSH配置(在本地命令行执行)

```bash
nano ~/.ssh/config
```

```
Host master #自定义
    HostName 211.81.48.139
    User liuzixuan

Host gpu #这个可以自定义
    HostName gpu #不要改
    User liuzixuan
    ProxyJump master #自定义，需要和第一行相同
```

4、保存并修改权限(在本地命令行执行)

```bash
chmod 600 ~/.ssh/config
```

之后在本地终端只需要`ssh gpu` 便可直接连接到GPU服务器
