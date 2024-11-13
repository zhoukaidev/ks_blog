## 简介

本文主要临时记录龙芯教育派相关备忘

## 实用命令

* 将loongson添加到sudo, `sudo usermod -a -G sudo loongson`

## 网址

* https://www.loongnix.cn/zh/embedded/EDUPI/
* https://my.oschina.net/chipo/blog/3077050
* https://www.iceasy.com/product/1638242397694160898
* 设置mips64el安装路径
    * deb http://ftp.nl.debian.org/debian/ oldstable main contrib non-free
    * deb http://ftp.nl.debian.org/debian/ oldstable-updates main contrib non-free
    * 在执行apt-get update出现无法验证签名，需要使用apt-get update --allow-insecure-repositories