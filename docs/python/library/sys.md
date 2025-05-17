# 简介

本文用于介绍`sys`模块的一些用法。

## 主要功能

* 获取系统类型

```
print(sys.platform)
```

* 库安装相关

```py
# 获取与平台独立的软件包的安装路径
print(sys.prefix)
# 获取与平台相关的软件包的安装路径
print(sys.exec_prefix)
```

## 参考文档

* [python3 sys module](https://docs.python.org/3/library/sys.html)
