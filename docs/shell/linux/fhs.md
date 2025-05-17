# 简介

FHS: Filesystem Hierarchy Standard

`FHS`定义了`linux发行版`中的目录结构及目录内容。绝大部分的`linux发行版`都会遵从该标准，这样使得在不同版本之间进行迁移更加容易。

## 目录结构

| 目录名称    |  主要用途    |
|-----------|--------------|
| `/tmp` | [Temporary file](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch03s18.html)  |
| `/var/tmp` | [Temporary files preserved between system reboots](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch05s15.html) |
| `/bin`| Essential user command binaries(for use by all users)|
|`/etc`| Host-specific system configuration（放置各种配置文件）|


## 参考手册

* [IBM FHS](https://www.ibm.com/developerworks/linux/library/l-lpic1-v3-104-7/)
* [linuxFoundaton fhs](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)
* [Filesystem Hierarchy Standard Specifications Archive](https://refspecs.linuxfoundation.org/fhs.shtml)
