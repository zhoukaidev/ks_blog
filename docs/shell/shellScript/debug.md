# 简介

该文用于介绍如何对`shell script`进行调试。

## 调试指令

* `bash -n script.sh`
* `bash -v script.sh`
* `bash -x script.sh`

| 参数    |  介绍  |
|---------|--------|
| `-n`    | 只做`shell script`的语法检查 |
| `-v`    | 在执行指令之前，先将指令进行输出 |
| `-x`    | 将每个被执行的指令都进行输出，以类似调用栈的形式输出待执行的指令及指令结果 |