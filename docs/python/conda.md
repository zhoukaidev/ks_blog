# 简介

本文主要介绍`conda`的相关使用方法。

## 命令

* 创建新的conda环境

```sh
#指定环境的名称和python的版本，其中python版本可以忽略
$ conda create --name myEnvironmentName python==3.7.0
```

* 激活指定的环境

```sh
$ conda activate myEnvironmentName
```
* 基于yml文件创建环境

```sh
$ conda env create --file myEnvironment.yml
```

* 退出相应的环境

```sh
$ conda deactivate
```

* 删除相应的环境

```sh
$ conda env remove -n myEnvironmentName
```
