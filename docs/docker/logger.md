# 简介

本文主要用于介绍`docker`下相关`Log`的配置情况。

Docker支持使用不同的`Log Driver`来管理docker application运行过程中的log.

## json-file

docker默认使用json-file作为log driver,当使用json-file的时候，log会默认生成json文件保存到主机中。

* 获取log存储路径

```sh
docker container inspect -f '{{.LogPath}}' <contianerId/Name>
```
