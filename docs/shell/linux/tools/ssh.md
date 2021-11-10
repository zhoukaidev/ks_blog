# 简介

本文用于介绍与`ssh`相关的使用方法。`ssh`主要包括两个部分:

* ssh client
    * ssh
    * scp
    * sftp
* ssh server

## ssh client

在`ssh client`中包括`scp`及`ssh`,其中`scp`用于文件传输，`ssh`用于远程连接。

### ssh

| 简介     |   指令    |
|----------|----------|
|连接remote meachine  | `ssh username@ip` / `ssh -l username ip`|
| `-p`  | 指定远程主机的端口 `ssh user@ip -p port`  | 
|退出连接   | `exit`  |

### scp

| 简介   |   指令   |
|--------|----------|
| 远程文件传输到本地 |  `scp user@ip:sourceFile TargetFolder` |
| 本地文件传输到远程服务器 | `scp SourceFile user@ip:targetFolder` |

### sftp

| 简介  |  指令   |
|-------|---------|
| 通过sftp连接到remote machine  | `sftp userName@HostAddress` |
| 查看remote machine上的文件列表 | `ls`  |
| 查看local machine上的文件列表  | `lls`  |
| 查看remote machine上的当前路径 |  `pwd`  |
| 查看local machine上的当前路径 | `lpwd`  |
| 切换remote machine上路径  |  `cd xxx`  |
| 切换local machine上的路径 | `lcd xxx`  |
| 下载remote machine上的文件 | `get remoteFile` |
| 下载remote machine上的文件夹 | `get -r remotefoler` |
| 上传local machine上的文件到remote machine | `put localFile` |
| 上传local machine上的文件夹到remote machine | `put -r localFolder` |

#### sftp参考文档

* [How to use sftp to securely transfer files with a remote server](https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server)
