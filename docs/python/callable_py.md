# 简介

本文用于介绍`python`中`callable`的类型。
这里的`callable`是指该对象能够像函数一些被调用。主要包括两个部分:

* 函数
* 可调用对象

## 函数

`python`中定义函数使用`def`关键字:

```py
#!/usr/bin/env python3

def sayHello(name):
    print('Hello ', name)
sayHello('spider man')
```

我们可以看到`sayHello`函数可以使用`sayHello()`的方式进行调用，第一种可调用对象。

## 可调用对象

我们在面向对象编程中,都是通过`object.method()`的方式进行调用，我们也可以实现一些可调用对象，
以`object()`的形式调用。

```py
#!/usr/bin/env python3

class Add(oject):
    def __init__(self, a, b):
        self.a = a
        self.b = b
    def __call__(self):
        print('a = ', a)
        print('b = ', b)
        return self.a + self.b

# 定义Add类型的对象
a = Add(2, 3)
# 调用a对象
a()
```

这里我们看到，我们通过为类定义`__call__`函数，来实现对象的可调用。
