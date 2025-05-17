# 简介

本文主要介绍`python`中不同类型的函数参数。

* 位置参数
* 可变参数
* 默认参数
* 命名参数(关键字参数)
* 位置参数+命名参数(限制参数名称)

## 位置参数

位置参数是最直接也最简单的,需要做的就是根据自己的需求定义所需要的参数。

需求: 我们需要一个函数来对两个数字就行求和，则需要定义两个参数。

```py
def my_sum(x,y):
    return x+y
```

## 可变参数

突然有一天，需求发生了变更，我们不仅需要支持两个数的求和，还需要支持任意个数的求和，此时我们需要使用可变参数来实现。

需求二: 定义一个函数，对任意参数个数进行求和。

```py
def my_sum(*args):
    _sum = 0
    for num in args:
        _sum = _sum + num
    return _sum
```

在定义可变参数的时候,我们将`*`符号放在参数名之前，此时参数变为可变参数。
我们对以上函数做一些小改动，在函数内部打印出`args`值看一下:

```py
def my_sum(*args):
    print(args)
    _sum = 0
    for num in args:
        _sum = _sum + num
    return _sum
```

通过打印出来的`args`可以看出，可变参数在函数内部是以`tuple`类型的数据存在的，所以我们可以通过`for num in args`的形式来访问内部的各个参数。

## 默认参数

默认参数是指为某些参数指定默认值，在函数调用的时候如果没有为该参数传入相应的值，则使用默认的参数值。

需求: 定义一个函数求某个数据的n次方，当未指定次方的时候，则求平方和。

```py
def power(num, n = 2):
    res = 1
    while n > 0:
        res = res * num
        n = n - 1
    return res
# 函数调用
power(3) # 求3的平方和
power(3,3) # 求3的立方和
```

## 命名参数

`命名参数`是指在传入参数的时候要同时指定`参数名称`及`参数值`。

在`可变参数`章节中，我们可以看到可变参数在函数内部被组织为`tuple`类型，命名参数在函数内部则被组织为`dictionary`类型。

在定义`可变参数`的时候，我们使用`*args`语法来定义，在定义命名参数的时候，我们需要使用`**kwargs`语法来定义。

* 命名参数使用`**`符号
* 可变参数使用`*`符号

```py
def person_info(**kwargs):
    print(kwargs)
    for key,value in kwargs.items():
        print(key, ":", value)
# 调用该函数，输出名称，年龄
person_info(name="spider man", age=23)
```

从以上打印的结果可以看出命名参数在函数内部是以`dictionary`形式存在的。

## 位置参数+命名参数(限制参数名称)

在定义该类型函数的时候，需要使用`*`作为分隔符，例程如下:

```py
def person(name,age,*,city):
    print("name:",name)
    print("age:",age)
    print("city:",city)

# 函数调用
# name,age为位置参数
# city为命名关键字参数
person("spider", 23, city="world")
```

`python`提供的`subprocess.run`函数原型如下:

```py
subprocess.run(args, *, stdin=None, input=None, stdout=None, stderr=None, capture_output=False, shell=False, cwd=None, timeout=None, check=False, encoding=None, errors=None, text=None, env=None, universal_newlines=None)
```

在`subprocess.run`函数原型中可以看到:

* `args`为位置参数
* `*`符号后面的命名关键字参数，其中参数名称已经被指定
