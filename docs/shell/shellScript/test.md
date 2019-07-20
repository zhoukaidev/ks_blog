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

| 操作符      |  描述      |    例程   | 英文记忆   | 比较符号  |
|------------|-----------|-----------|-------------|----------|
| -eq        | 比较两个值是否相等,相等则返回true | [ $a -eq $b ] | equal | = |
| -ne        | 比较两个值是否相等，相等则返回false | [ $a -ne $b ] | not equal | != |
| -gt        | 比较两个值大小，左值大于右值，则返回true | [ $a -gt $b ] | greater than | > |
| -lt        | 比较两个值大小，左值小于右值，返回true  | [ $a -lt $b ] | less than | <  |
| -ge        | 大于等于比较, 左值大于等于右值，返回true | [$a -ge $b] | greater than or equal | >= |
| -le        | 小于等于比较，左值小于等于右值，返回true | [ $a -le $b ] | less than or equal  | <= |

### 数字类型运算符例程

* `'-eq'`,`'-ne'` 操作符

```sh
#!/bin/bash
A=10
B=10
# 比较A与B的值是否相等
if [ $A -eq $B]; then
    echo "A is equal to B"
else
    echo "A is not equal to B"
fi

C=10
D=20
# 比较C与D的值是否不相等
if [ $C -ne $D ]; then
    echo "C is not equal to D"
else
    echo "C is equal to D"
fi
```

* `'-gt'`,`'-lt'` 操作符
  
```sh
#!/bin/bash
A=20
B=10
# 比较A与B的值是否相等
if [ $A -gt $B]; then
    echo "A is greater than to B"
else
    echo "A is not greater than to B"
fi

C=10
D=20
# 比较C与D的值是否不相等
if [ $C -lt $D ]; then
    echo "C is less than to D"
else
    echo "C is not less than to D"
fi
```

* `'-ge'`,`'-le'`类似

## 布尔运算符

`'['` 指令支持 **与**，**或**，**非** 运算符。

| 操作符     |  描述    | 例程  | 比较符号 |
|-----------|----------|-------|---------|
| !         | 非运算符 | [ ! false ] | !   |
| -o        | 或运算符 | [ $a -eq $b -o $c -eq $d ] | \|\| |
| -a        | 与运算符 | [ $a -eq $b -a $c -eq $d ] | &&   |

### 布尔运算符例程

* `'!'` 运算符
  
```sh
#/bin/bash
A=10
B=10
if [ ! $A -eq $B ]; then
    echo "A is not equal to B"
else
    echo "A is equal to B"
fi
```

* `'-o'`, `'-a'` 运算符

```sh
#!/bin/bash

A=10
B=20

if [ $A -eq 10 -o $B -eq 10]; then
    echo "A = 10 or B = 10"
else
    echo "A !=10 and B != 10"
fi

if [ $A -eq 10 -a $B -eq 20]; then
    echo "A = 10 and B = 20"
else
    echo "A != 10 or B !=20"
fi
```

## 字符串比较运算符

针对字符串共有五种比较不同的比较运算符:

| 操作符   |  描述    |   例程  |
|---------|----------|---------|
| =      | 两个字符串值是否相同 | [ $A = $B ] |
| !=    | 两个字符串是否不相同  | [ $A != $B ] |
| -z    | 字符串长度为0，返回true | [ -z $A ] |
| -n    | 字符串长度不为0,返回true | [ -n $A ] |
| str   | str不为空，则返回true   | [ $A ] |

### 字符串比较运算符例程

* '`=`',`'!='` 运算符

```sh
#!/bin/bash

A="hello"
B="hello"
C="world"

if [ $A = $B ]; then
    echo "A is equal to B"
    echo "A = B = $A"
else
    echo "A is not equal to B"
    echo "A = $A, B = $B"
fi

if [ $B != $C ]; then
    echo "B is not equal to C"
    echo "B = $B, C = $C"
else
    echo "B is equal to C"
    echo "B = C = $B"
fi
```

* `'-z'`,`'-n'` 运算符

```sh
#!/bin/bash

A='hello'
B=''
if [ -n $A ]; then
    echo "A's lenght is greater than zero"
else
    echo "A's length is zero"
fi

if [ -z $B ]; then  
    echo "B's length is zero"
else
    echo "B's length is greater than zero"
fi
```

## 参考手册

* [shell Basic Operator](https://www.tutorialspoint.com/unix/unix-basic-operators.htm)
* [shell scripting Tutorial/Test](https://www.shellscript.sh/test.html)

