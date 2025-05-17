# 简介

本文主要用于介绍在`python`中关于`类`的相关基础概念。

在大部分面向对象编程语言中，当我们谈到类的概念的时候，都会提到类的四个特性:

* 封装
* 继承
* 多态
* 重载

我们也按照这种节奏来介绍一下`python`中如何实现以上的这些特性。
本文我们会介绍在`python`中如何实现`封装`及`继承`。

## 封装

封装是指将数据以及对数据的相关操作封装在一起。其实就是如何定义一个最基本的类。

```py
class Person(object):
    def __init__(self):
        self.name = "spider man"
        self.age = 23
```

以上例程可以看出:

* 定义一个类使用`class`关键字，然后后面紧跟`类名`
* `类名`之后的`object`代表该Person类继承于`object`
* `__init__`相当于类的构造函数,该函数的第一个参数必须是`self`

完善一下上面的例子,多添加几个方法:

```py
class Person(object):
    def __init__(self):
        self.name = "spider man"
        self.age = 23
    # 添加myName方法，用于打印该Person的名字
    def myName(self):
        print("My name is ", self.name)
    # 添加myAge方法，用于打印该Person的年龄
    def myAge(self):
        print("My age is ", self.age)

# 创建一个Person的示例
p = Person()
# 调用myName方法，打印出p的名字
p.myName()
# 调用myAge方法，打印p的年龄
p.myAge()
```

## 继承

在继承体系中分为`父类`与`子类`，子类可以继承父类的属性与方法，并在此基础上添加属于自己的独特方法。

比如我们有一个`Person`类，用来标识人类的通用的一些属性及方法，比如年龄，性别等。

`Student`类可以继承`Person`类，并在此的基础上添加`学号`,`班级`等属性及一些独特的方法。

首先我们定义一个`Person`类:

```py
class Person(object):
    def goHome(self):
        print("Person is go home...")
```

我们来定义一个`Student`类，该类继承自`Person`:

```py
class Student(Person):
    pass
```

我们定义了`Student`类，在该类内部并没有定义任何函数，但依然可以继承`Person`的`goHome`方法。

```py
#例程
# 定义Person类，并调用goHome
p = Person()
p.goHome()
# 定义Student类，并调用goHome
stu = Student()
stu.goHome()
```

上面我们介绍了继承最基本的概念，有没有注意到上面我们并没有添加构造函数这些。
现在我们把`委托构造函数`加进来。

```py
# 在构造Person类的时候，需要提供`name`,`age`
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

# 相比于`Person`类，`Student`类添加了`studentId`属性
# 在Student的构造函数里，我们调用了Person的构造函数，来添加Student的name,age属性
class Student(Person):
    def __init__(self, name, age, studentId):
        Person.__init__(self, name, age)
        self.studentId = studentId

p = Person('spider man', 23)
stu = Student('spider man2', 23, '201203')
print("Person: ", p.name, p.age)
print("Student: ", stu.name, stu.age, stu.studentId)
```
