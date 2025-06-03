# 简介

本文主要介绍 `source` 命令在linux下的作用。

`source` 命令用于从制定的文件中读取并执行相关的指令。

`source` 是大部分的shell内置的指令。

## 基本语法

```sh
source fileName [Arguments]
```

* `source` 与 `.` (一个点) 是同一个指令

## 例程

* 创建一个`test.txt`,并写入`echo`指令
```sh
echo "hello first day" >> test.txt
echo "hello second day" >> test.txt
```
* 通过`source`指令执行该文件

```sh
source test.txt # source command
. test.txt  # . command
```

* 自行查看该指令的输出结果 enjoy :)

## 扩展

在编写`shell script`的时候，我们有时候可能会引用外部的脚本库，还记得是怎么引用的吗？

1. 例如我们创建一个log库: `log.sh`

```sh
#!/bin/bash
# log.sh

logInfo(){
    DATETIME=$(date)
    echo "${DATETIME}: $1"
}
```

2. 在脚本`run.sh`中引用该`log.sh`中定义的函数

```sh
#!/bin/bash
# run.sh

. log.sh
logInfo "Hello world!!!"
```

在这里我们就使用了 `.` 指令。*(注意 `.` 与 `source` 是同一个指令哦)*