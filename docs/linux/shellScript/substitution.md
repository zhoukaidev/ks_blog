# 简介

本文用于介绍在`shell`中用于替换的相关指令。

## 变量替换

`变量替换`是指在定义变量之后，在后续脚本置中如何使用该变量。
使用变量的方式有两种:

* ${variable}
* $variable

以上两种方式都可以访问变量，使用`$`符作为前缀，`{}`为可选符号，`variable`为变量名称。

```sh
HELLO="hello world"
echo $HELLO
echo ${HELLO}
```

## 指令替换

`指令替换`是将脚本中定义的字符串当作需要运行的指令，并将指令输出替代原先的字符串。
使用指令替换有两种方式:

* \`command\`
* $(command)

```sh
PATH=`pwd`
DATE=$(date)
echo ${PATH}
echo ${DATE}
```

