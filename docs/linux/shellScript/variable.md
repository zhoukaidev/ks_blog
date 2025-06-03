# 简介

本文中，我们会主要讨论两个部分:

* 普通变量
  * 定义变量
  * 删除变量
* 变量的访问
* `shell`脚本中的特殊变量

在`shell`脚本中，特殊变量是指内置的一些变量名称，这些变量有特定的意义，除此以外，
我们定义的其他变量都是普通变量。

## 普通变量

### 定义变量

在shell脚本中,定义变量的语法格式如下:

```sh
variable_name=variable_value
```

在这里有几点需要注意:

* `"variable_name"`,`"="`及`"variable_value"`之间不存在任何空间
* 变量名一般使用纯大写字母

```sh
#!/bin/sh
#定义两个变量并赋值
COUNTRY="China"
NAME="kai"
```

### 删除变量

当我们定义变量之后,我们也可以删除相应的变量，在删除相应的变量后，当我们再次引用该变量的时候，
该变量的值变为空。

删除变量的语法:

```sh
unset variable_name
```

以下的例程中，我们首先定义一个变量，然后在删除改变量:

```sh
#!/bin/sh
COUNTRY="china"
#该语法为变量访问，后续进行介绍
echo $COUNTRY 
unset COUNTRY
echo $COUNTRY
```

## 变量访问

为了访问脚本中定义变量的值,需要在变量名前使用`$`符号。

```sh
#!/bin/sh

NAME="kai.zhou"
# 直接访问变量
# 输出值为 kai.zhou
echo $NAME

# 变量的拼接
# 输出值为 hello_kai.zhou
echo "hello_${NAME}"
```
## `shell`脚本中的特殊变量

| 变量名称   |   变量含义   |
|-----------|--------------|
| $0        | 目前脚本名称  | 
| $n        | n的值为(1...n), `$1`代表第一个参数, $2第二个参数...|
| $#        | 传入的参数总数量  |
| $?        | 上次执行的命令的返回值  |
| $*        | 所有参数一起被双引号包围  |
| $@        | 每个参数单独被双引号包围  | 
| ...       | ... |


```sh
#!/bin/sh
# variable.sh
echo "The filename of current script: $0"
echo "The first parameter: $1"
echo "The second parameter: $2"
echo "The number of argument supplied to script: $#"
echo "The exit status of the last command: $?"
echo "All argument are double quoted: $*"
echo "All arguments are individually double quoted: $@"
```

```sh
# run variable.sh
$ ./variable.sh hello world
```
