# 简介

本文用于介绍有关`ssh server`的相关配置及使用方法。

## 指令集

* 查看`ssh server`状态

```sh
$ systemctl status sshd
```

* 添加新的`public key`

```sh
# 添加公钥到authorized_key
$ cat myPublicKey.pub >> ~/.ssh/authorized_key

# sshd重新读取配置文件
$ systemctl reload sshd
```
