# 简介

本文用于介绍`python`中关于函数定义及调用的各种语法及规则。

本文的介绍主要分为以下部分:

* 函数定义
  * 如何定义函数
  * 如何定义函数返回值


## 函数定义

### 如何定义函数

在`python`中定义函数需要使用`def`关键字，基本语法如下:

```py
def function_name(function_parameters):
    function_body
```
定义一个函数用来打印姓名:

函数名称: `my_name`   
函数参数: `name`
返回值: `无`,(当没有返回值时,python默认返回None)

```py
def my_name(name):
    print("My name is ", name)

#调用my_name函数
my_name("spider man")
```

### 如何定义函数返回值

和其他编程语言类似，在`python`中使用`return`来完成函数返回值。

在`python`中我们可以返回一个值或同时返回多个值。

* 返回一个值

```py
# 定义求和函数,返回一个值
def my_sum(x, y):
    return x+y

#调用my_sum函数,并打印两个数之和
_sum = my_sum(1,2)
print(_sum)
```
`my_sum`是一个简单的求和函数，返回值为两个数之和，只有一个返回值。

* 返回多个值

```py
#定义求和函数，返回参数及两者之和，返回多个值的情况
def my_sum_2(x,y):
    return x,y,x+y

_sum = my_sum_2(2,3)
print(_sum)
```
虽然我们可以使用`return`语句来返回多个值，但通过`print(_sum)`语句，我们可以看出，实际上返回的是一个`tuple`类型，该`tuple`对象包含了需要返回的三个值。

