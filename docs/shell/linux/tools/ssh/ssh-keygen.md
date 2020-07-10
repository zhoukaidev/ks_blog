# 简介

`ssh-keygen`是用于生成,管理以及转换授权密钥的工具。


## 指令

`ssh-keygen`支持很多不同的参数组合，我也会随着学习的深入来持续更新该文章。

* 生成RSA密钥

在不添加任何参数的情况下,默认会生成RAS密钥.

```sh
$ ssh-keygen
xxxx
```

* 生成指定类型的密钥

具体支持的类型可以通过`man ssh-keygen`查看。

```sh
# 生成DSA密钥
$ ssh-keygen -t dsa
```

