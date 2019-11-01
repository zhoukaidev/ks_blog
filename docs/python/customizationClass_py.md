# 简介

本文主要介绍`python`中关于`定制类(customizaiton class)`的概念。

更详细的内容，可以参考[python Basic customization](https://docs.python.org/3/reference/datamodel.html#basic-customization)。

## 前期思考

先来一小段代码暖身:

```py
#!/usr/bin/env python3

_list = [1, 2, 3, 4]
print(_list)
length = len(_list)
print(length)
```

上面这段代码的输出值是:

```sh
[1, 2, 3, 4]
4
```

我们写一个自定义类，重新调用上面的代码:

```py
#!/usr/bin/env python3

class Person(object):
    pass

person = Person()
print(person)
length = len(person)
print(length)
```

上面的代码在我电脑上的输出值为:

```py
<_main__.Person object at 0x102203278>
Traceback(most recent call last):
...
TyepError: object of type 'Person' has no len
```

我们可以看到，`print(person)`的输出值为`<_main__.Person object at 0x102203278>`, `length = len(person)`代码运行出错。

思考一下:

* 为什么打印的`_list`和`person`的值会不一样?
* 为什么`len(person)`会报错?

## 让`Person`支持print

还记得在`python`中，类的构造函数形式是`__init__`,像这种在函数名称前后各有两个下划线的函数，是`python`中的保留函数名称，会在某些情况下调用。

让我们为`Person`函数实现一个`__str__`函数:

```py
class Person(object):
    def __str__(self):
        return "I am a person"

person = Person()
print(person)
```

以上代码的输出值为:
```sh
I am a person
```

我们重写了`__str__`函数，这是我们调用`print`函数的时候，就可以将`__str__`返回值打印出来。
这也就是上面代码中`_list`可以打印出`[1, 2, 3, 4]`的愿意，因为它们按照自己的需要重写了`__str__`函数。

## Person支持`len`函数

```py
class Person(object):
    def __len__(self):
        return 0

person = Person()
length = len(person)
print(length)
```

运行上面的代码输出值为:
```sh
0
```

发现没， `len`函数最终调用了`Person`的`__len__`函数，并将`__len__`函数的返回值进行返回。

## 总结

我们通过重写不同类型`__xx__`函数，来为我们的类提供不同的功能，这也是定制类的用法所在。当然`__xx__`形式的函数有很多，我们具体就要参考官方文档了。

* [官方文档](https://docs.python.org/3/reference/datamodel.html#basic-customization)