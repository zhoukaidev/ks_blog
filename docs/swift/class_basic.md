## 类基本语法

* `class`关键字定义类
* 访问类的属性
* 判断两个类是否相等

使用`class`关键字来定义基本类:

```swift
class student {
    var name: String = "Joe"
    var age: Int = 21
    var identity: String = "2012483"
}

let stu1 = student() //创建实例
```

使用'`.`'运算符访问类属性:

```swift
class student {
    var name: String = "Joe"
    var age: Int = 21
    var identity: String = "2012483"
}

let stu1 = student() //创建实例
print(stu1.name)
print(stu1.age)
print(stu1.identity)
```

使用"`===`" 及 "`!==`" 运算符来进行两个实例的比较:

在类实例赋值的过程中，一般是以引用的方式，在使用这两个运算符时，是比较两个变量是否指向同一个地址空间.

```swift
class student {
    var name: String = "Joe"
    var age: Int = 21
    var identity: String = "2012483"
}

var stu1 = student() //创建实例
var stu2 = stu1
var otherStu = student()

print(stu1 === stu2) //true
print(stu1 === otherStu) // false
print(stu1 !== otherStu) // true
```