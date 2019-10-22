# 简介

本文用于介绍`shell script`中的输入，输出重定向的相关概念。

## 输出重定向

输出流分为两个部分:

* 标准输出(STDOUT)
* 错误输出(STDERR)

在`shell script`中，需要使用不同的语法来进行不同输出的重定向。

| 语法   | 含义 |
|--------|------|
| `cmd 1> file.log` | 清除file.log,并将标准输出重定向到file.log中 |
| `cmd 1>> file.log` | 将标准输出追加到file.log中 |
| `cmd 2> error.log` | 清除error.log,并将错误输出重定向到error.log中 |
| `cmd 2>> error.log` | 将错误输出追加到error.log中 | 