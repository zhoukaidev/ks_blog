# 简介

本文主要用于记录在日常工作中常用的各种 `linux` 指令。

## 系统信息查看

| 指令   | 参考文档   |
|--------|-----------|
| `uname`(unix name) | [man page](https://linux.die.net/man/1/uname) |
| --  | `-r --kernel-release` 获取kernel版本  |

## 通用指令

| 指令  |  简述   |  参考文档  |
|-------|---------|-----------|
| `which` | show the full path of shell command | [man which](https://linux.die.net/man/1/which) |
| `apt-get`| managing software packages | [source.list][aptSourceList], [Usage][aptCommand] |
| `tar` & `gzip` | archive and compress file or folder | [tar gzip](tools/tarGzip.md) |
| `source` | execute command that defined in file   | [source](tools/source.md) |
| `env` | dispaly or set environment variable | [tutroial](tools/env.md) |

[aptSourceList]: https://wiki.debian.org/SourcesList
[aptCommand]: tools/apt.md

## 编码

| 指令  | 简述    |  参考文档  |
|-------|---------|-----------|
| `base32` | base32 encode/decode data | `man base32` |
| `base64` | base64 encode/decode data  | `man base64`  |

## 文件操作

| 指令  | 简述  | 参考文档  |
|------|--------|----------|
| `dd` | stands for "data duplicator" | `man dd` |

## 内存
| 指令  | 简述  | 参考文档  |
|------|--------|----------|
| `free` | "free -g -h -t",内存使用率 | `free --help` |


