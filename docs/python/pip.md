# 简介

本文主要介绍`pip`的一些常用的方法。

## 常用的操作指令

* 显示安装包的版本

```sh
$ pip show mypackage
```

* 配置代理

```sh
$ pip install myPackage --proxy=http://proxyurl:port
```

* 安装指定版本的软件包

```sh
$ pip install myPackage=0.1.0
```

* 设置镜像

```sh
#临时使用
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package

# 设为默认
python -m pip install --upgrade pip
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

#使用清华镜像升级pip
python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple --upgrade pip
```

[使用清华镜像](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)

参考 https://blog.csdn.net/u012887259/article/details/102804707

* 创建pypi安装包
  * 参考vmilog-py仓库的setup.py文件
  * 参考https://towardsdatascience.com/how-to-upload-your-python-package-to-pypi-de1b363a1b3
