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

* 获取指定公钥的fingerprint

```sh
# 适用 -l 来获取
# -f 指定公钥文件, -l 指定获取fingerprint
$ ssh-keygen -l -f xxx.pub
```

* 指定fingerprint的编码格式

```sh
# 当使用putty登陆时,显示的fingerprint适用MD5编码进行显示
# 在ssh-keygen也可以通过 -E 指定显示的格式
$ ssh-keygen -E md5 -l -f xxx.pub
```
