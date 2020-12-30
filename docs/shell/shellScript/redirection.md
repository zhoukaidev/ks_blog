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

### 文件描述符

文件描述符是使用一个正数来表示一个打开的文件，前面所说的`STDOUT`及`STDERR`也有各自的
文件描述符。

| 文件名   | 描述符  |
|----------|--------|
| STDOUT    | 1  |
| STDERR    | 2   |

当需要同时重定向`STDOUT`和`STDERR`时，可以使用如下语法:

```sh
ls dir1/ dir2/ > contents.txt 2>&1
```

## 输入重定向

输入流主要是指`STDIN`模块，通过终端进行输入。

正常情况下，程序会使用`stdin`从终端来读取输入，但有时候我们需要对输入进行重定向，比如从文件中来获取输入等。

```sh
# 输出重定向
$ who > users
# 输入重定向
$ wc -l < users
```

## 总结

* `>` 为`STDOUT`重定向符， `>>`将`STDOUT`输出追加到一个文件中
* `2>`为`STDERR`重定向符, `2>>`将`STDERR`输出追加到一个文件中
* `>&`为将一个输出重定向到另外一个输出, `2>&1`代表将`STDERR`输出重定向到`STDOUT`, `1>&2`与之相反。
