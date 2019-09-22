# 简介

本文用于介绍与`ssh`相关的使用方法。`ssh`主要包括两个部分:

* ssh client
  * ssh
  * scp
* ssh server


## ssh client

在`ssh client`中包括`scp`及`ssh`,其中`scp`用于文件传输，`ssh`用于远程连接。

### ssh

| 简介     |   指令    |
|----------|----------|
|连接remote meachine  | `ssh username@ip` / `ssh -l username ip`|
|退出连接   | `exit`  |

### scp

| 简介   |   指令   |
|--------|----------|
| 文件传输 |  `scp user@ip:sourceFile TargetFolder`
