# 简介

在上篇文章中，我们已经介绍了`python`的如下两种特性:

* 封装
* 继承

在本文中，我们会介绍类的另外两种特性:

* 多态
* 重载

## 多态

还记得多态是什么吗？

> 多态是指通过相同的接口类型来动态的调用不同的底层实现。在C++中，多态需要通过虚函数来实现。

来看一下`python`对于多态的实现:

```py
 #!/usr/bin/env python3
 
 class Animal(object):
         def run(self):
                 print("Animal is running...")
 
 class Cat(Animal):
         def run(self):
                 print("Cat is running...")
 
 class Dog(Animal):
         def run(self):
                 print("Dog is running...")
 
 def running(animal):
         animal.run()
 
 animal = Animal()
 dog = Dog()
 cat = Cat()
 
 running(animal)
 running(dog)
 running(cat)
```

从以上代码中，我们可以看到`Cat`与`Dog`都继承`Animal`类， 并重写了`run`函数，分别将三个实例对象传入`running`函数，有没有注意到`running`函数可以根据不同的类型来调用不同的函数。这意味着我们可以继续继承`Animal`类型产生更多的对象，这些对象都可以在`running`函数中使用。

### 鸭子类型

在上面的代码中，我们强调继承`Animal`类，然后重新实现`run`函数来实现多态。在`running`函数中传入`Aniaml`类型的实例，
来调用该实例的`run`函数。

那我们如果传入的对象并不是`Animal`类型，该函数运行会出错吗?

```py
class Car(object):
    def run(self):
        print("Car is running...")
    
car = Car()
running(car)
```

可以看出，上面代码依然可以运行，这就是鸭子类型的力量。我们需要一个会`run`的`Animal`,但我们传入的对象即使不是`Animal`,只要这个对象可以`run`,我们的代码就依然可以运行。

其实本质上是因为`python`是一门动态语言。

## 重载

`python`中并不支持重载的概念。