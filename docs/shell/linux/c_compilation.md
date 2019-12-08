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

我们先来创建一个源文件`compilation.c`, 后续所有的操作都基于该文件来进行：

```c
#include <stdio.h>

#define FORMAT_STRING "%s"
#define MESSAGE "Hello, World\n"

int main(int argc, char *argv[])
{
   printf(FORMAT_STRING, MESSAGE);
   return 0;
}
```

## 预处理

在编写的源码里会有很多`#include`, `#define`等指示符，预处理阶段主要用于处理这些指示符。

这些`指示符`所代表的实际源码会被替换到需要编译的源文件中。

* 显示预处理后的代码

```sh
gcc -E -P xx.c
```
