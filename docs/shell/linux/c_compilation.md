# 简介

本文主要用于介绍`C/C++`的编译流程。

`C`语言的编译流程主要分为四个部分:

* preprocessing(预处理)
* compilation(编译)
* assembly(汇编)
* linking(链接)

---

![compilation phases](assert/compilation-phase.jpg)

---

## 预处理

在编写的源码里会有很多`#include`, `#define`等指示符，预处理阶段会使用这些指示符所代码的源码替换到源文件中。

* 显示预处理后的代码

```sh
gcc -E -P xx.c
```
