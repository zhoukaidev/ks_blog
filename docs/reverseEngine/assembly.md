# 汇编语言简介

随着各种高级语言(c/c++/java等)及脚本语言(js/python等)的发展,接触汇编语言的机会越来越少。
本节主要用于介绍汇编语言的基础知识及语法，扎实的汇编语言知识对于逆向工程及理解操作系统会有很大的帮助。
汇编语言从在不同的语法形式，这里我们会介绍两种:

* Intel syntax
* AT&T syntax

其中在`Intel syntax`主要使用在`windows`，`AT&T syntax`大部分用在`Linux`平台。
当然使用何种汇编语言语法还是依赖于使用何种汇编器的。

`AT&T syntax`使用在`GNU AS`汇编器中，`GNU AS`也经常简称为`GAS`.

## 语法介绍

### AT&T语法

| 特性   |  简介     |  示例代码   | 代码含义 | 
|-----------|-----------|---------|----------|
|  寄存器(register)   | 使用`%`修饰寄存器   | MOV %EAX, %ECX | 将EAX值移动到ECX |
|  立即数(immediate value)   | 使用`$`修饰立即数  | MOV $3, %EAX   | 将3移动到EAX   |
|  内存地址访问      | `x(%寄存器)` 形式 | MOV 4(%EAX), %ECX | 将(EAX+4)所指向的内存地址里的数据移动到ECX中，类似于`ECX = *(EAX+4)` |



### 基本汇编指令


| 指令   |  简介    | Intel语法 | AT&T语法  |  示例代码含义 |
|-------|----------|-----------|-----------|--------------|
| MOV   |   --     | ---       |   --------|--------------|

## 参考文档

* [Assembly Tutorial from tutorialpoint](https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm)
