# 简介

本文用于介绍`python`中类所涉及的两种不同的属性:

* 类属性
* 实例属性

## 实例属性

实例属性是指该属性归某个实例所有，不同的实例对象之间并不共享这些属性。

来个例程理解以下:

```py
class Student(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student('bob', 21)
s2 = Student('john', 25)
print('s1 name: %s, age: %s' % (s1.name, s1.age))
print('s2 name: %s, age: %s' % (s2.name, s2.age))

# 修改s1的name,age属性
s1.age = 28
s1.name = 'tom'
print('s1 name: %s, age: %s' % (s1.name, s1.age))
print('s2 name: %s, age: %s' % (s2.name, s2.age))
```

输出值:

```py
s1 name: bob, age: 21
s2 name: john, age: 25
s1 name: tom, age: 28
s2 name: john, age: 25
```

我们修改了`s1`的`name`与`age`,但并不影响`s2`, 这就是所谓的`实例属性`。

## 类属性

类属性归类所有，所有的实例共享这个属性。当创建一个实例的时候，我们并不会重新创建这个属性的内存空间。

我们希望统计共创建了多少个`Student`:

```py
class Student(object):
    #在此处来创建`类属性`
    _count = 0
    def __init__(self, name, age):
        self.name = name
        self.age = age
        # 创建对象的时候，为类属性增加1
        Student._count = Student._count + 1

s1 = Student('tom1', 21)
print(Student._count)
s2 = Student('tom2', 22)
print(Student._count)
```

输出值:

```py
1
2
```

从以上结果可以看出，`类属性`所有的对象共享，每个`Student`对象都可以修改该属性。

## 修改类属性

我们无法通过使用对象的方式来修改类属性,当尝试使用对象来修改类属性的时候,实际上发生的事情是为该对象增加了一个新的属性。

修改类属性需要使用`类`来引用该属性。

```py
class Student(object):
    name = "Student"
    def __init__(self, age):
        self.age = age

stu = Student(13)
print(stu.name)
print(stu.age)
stu.name="mynewname"
print(stu.name)
print(Student.name) # 使用类来修改类属性
```

输出值为:

```py
Student
13
mynewname
Student
```

