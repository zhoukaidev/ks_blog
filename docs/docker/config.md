# 简介

本文主要用于介绍有关`docker`的相关配置。

## 非root用户使用docker

```sh
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

## proxy配置

针对`linux`系统,添加`~/.docker/config.json`文件，并做如下的配置

```sh
{
 "proxies":
 {
   "default":
   {
     "httpProxy": "http://127.0.0.1:3001",
     "httpsProxy": "http://127.0.0.1:3001",
     "noProxy": "*.test.example.com,.example2.com"
   }
 }
}
```

## 配置registry镜像

因为国内网络的原因，有时候直接从`hub.docker.com`上pull镜像的时候，会出现网络不稳定等问题，所以我们需要添加镜像，让
我们的docker从国内的镜像网站中来下载image.

修改`/etc/docker/daemon.json`文件:

```sh
{
  "registry-mirrors": ["https://<my-docker-mirror-host>"]
}
```
