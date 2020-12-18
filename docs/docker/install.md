# 简介

本文主要介绍不同操作系统下`docker`的安装方法。

## Linux

* 卸载老版本的docker,老版本的docker被称为`docker`,`docker.io`,`docker-enginee`

```sh
sudo apt-get remove docker docker-enginee docker.io containerd runc
```

* 卸载新版本的`docker`相关软件

```sh
sudo apt-get purge docker-ce docker-ce-cli containerd.io
```

> 以上指令不会删除image, container, volue,network等，如果想要全新的环境
> 需要`sudo rm -rf /var/lib/docker`删除相应的文件

* 安装需要的依赖软件

```sh
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

* 添加docker官方的GPG key

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

> 验证gpg key: `sudo apt-key fingerprint 0EBFCD88`

* 添加docker的repository到apt的source里面去

```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

* 更新`apt`及安装docker

```sh
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

> 此处会安装最新的dockr

## 参考文档

* [install docker on ubuntu](https://docs.docker.com/engine/install/ubuntu/)
