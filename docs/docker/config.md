# 简介

本文主要用于介绍有关`docker`的相关配置。

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
