# 简介

本文用于介绍软件包管理系统:

* `dpkg`
* `apt-get`

## 设置proxy

添加 `/etc/apt/apt.conf.d/proxy.conf`文件

```shell
Acqurire {
  HTTP::proxy "<add your proxy address here>"
}
```
## 添加软件源

TODO

## apt

* `apt-get`
* `apt-cache`
  
| 指令      |    用途     |
|-----------|-------------|
| `apt-get update` | 更新本地软件包数据库  |
| `apt-get upgrade`  |  下载并安装本系统已有的软件包的最新版本    |
| `apt-get install xxx` | 安装软件   |
| `apt-get remove`  | 卸载特定的软件   |
| `apt-get clean`  |  删除所有已下载的包文件  |
| `apt-get source`  | 下载特定的软件源代码   |


* apt-get(Advanced Package Tool)
    * sudo apt-get update(used to update datebase)
    * sudo apt-get upgrade(used to upgrade package)
    * sudo apt-get upgrade <packageName\>
    * sudo apt-get install <\pakcageName>
    * sudo apt-get install <\packageName> --no-upgrade
    * sudo apt-get install <\packageName> --only-upgrade
    * sudo apt-get remove <\packageName>
    * sudo apt-get purge <\packageName>
    * sudo apt-get clean
    * sudo apt-get autoclean
    * sudo apt-get autoremove
        * installing
        * upgrading
        * clean
* apt-cache
    * finding new packages
    * dpkg packaging system
