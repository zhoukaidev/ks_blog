# 简介

本文主要用于介绍`Linux`下`apt`的使用方法。

## 设置proxy

添加 `/etc/apt/apt.conf.d/proxy.conf`文件

```shell
Acqurire {
  HTTP::proxy "http://web-proxy.us.softwaregrp.net:8080"
}
```
