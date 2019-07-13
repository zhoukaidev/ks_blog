## 简介

该文档用于介绍`shell script`中用于条件判断的相关语法及规则。

在shell脚本中我们我们会经常使用判断语句，例如判断字符串是否为空，判断两个整数是否相同等等。
这里经常使用的就是`test`命令, 但是在shell脚本中, 我们很少可以看到`test`命令，因为`test`
指令有另外一个别名`[`。

## '[' 指令

在讲解`shell脚本`中条件判断之前，我们需要先了解有关`'['`指令的相关信息。

```sh
$ type [  # 看到'['是一个shell内置指令
[ is a shell builtin

$ which [
/usr/bin/[

#查看关于'['指令的介绍
$ man [
...
```

从这里可以看出, `'['`实际上为shell的内置指令，所以当使用该指令的时候，必须在该指令
后面放置空格。

```sh
# 在这个指令中, '['与'$foo'之间不包含空格，所以不能正常工作
# 因为'['本身是一个内置指令
[$foo = "bar" ]
```

此处需要修改为:

```sh
# '['与'$foo'之间需要包含空格
# 意味着在调用指令及传入相应的参数
[ $foo = "bar" ]
```

## 数字类型运算符

`'['` 指令包含一些针对数字类型进行支持的操作符。这些操作符对于字符串类型不支持。

| 操作符      |  描述      |    例程   | 英文记忆   |
|------------|-----------|-----------|-------------|
| -eq        | 比较两个值是否相等,相等则返回true | [ $a -eq $b ] | equal |
| -ne        | 比较两个值是否相等，相等则返回false | [ $a -ne $b ] | not equal |
| -gt        | 比较两个值的大小，左值大于右值，则返回true | [ $a -gt $b ] | greater than |





## 参考手册

* [shell Basic Operator](https://www.tutorialspoint.com/unix/unix-basic-operators.htm)
* [shell scripting Tutorial/Test](https://www.shellscript.sh/test.html)

