# 简介

本文用于介绍`gcc`中常用的一些参数定义。

## 添加头文件路径

```sh
gcc -I(dir)
```

* 例程请参考[这里](../../../sampleCode/gcc/includeHeader/build.sh)

## 调用外部函数库

```sh
gcc -l(libName) -L(libPath)
```
* -l: 链接某个函数库,如`-lm`是指`libm.so`或`-libm.a`库，其中`lib`及`.so/.a`可省略
* -L: 寻找函数库的路径, 如`-L/path`是指除了默认链接库路径也可以到`/path`路径下寻找该函数库

## 源码到汇编

```sh
gcc -S test.c
```

## 预处理阶段

```sh
gcc -E -P test.c
```

## 生成调试信息

```sh
gcc -g sourceFile
```

> -g: generate source level debug information

