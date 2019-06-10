## 类的方法分类

> 区分术语`函数`与`方法`:
>
> 在全局空间中使用`func`关键字定义一连串指令集称为`函数(functions)`。
>
> 在类中定义一个函数，使得该函数与特定的类相关联,此函数我们称为`方法(Methods)`.

* 实例方法(Instance Methods)
* 类方法(Type Methods)
* 方法中的`self`属性

### 实例方法

实例方法是指通过类实例可以调用的方法。

```swift
class student {
    var name:String
    var age:Int
    init(name:String, age: Int) {
        self.name = name
        self.age = age
    }

    func printInfo () {
        print("name: \(self.name)")
        print("age: \(self.age)")
    }
}

var stu = student(name: "tom", age: 18)
stu.printInfo()   // 通过实例调用内部方法
```

### 类方法

类方法只能通过定义的`类`来直接访问，不能通过类实例来访问。

定义`类方法`需要使用`static`关键字。

```swift
class student {
    var name:String
    var age:Int
    init(name:String, age: Int) {
        self.name = name
        self.age = age
    }
   // 实例方法
    func printInfo () {
        print("name: \(self.name)")
        print("age: \(self.age)")
    }

   //类方法
   //使用static 关键字
   static func printWelcome() {
       print("Welcome query system");
   }
    
}
student.printWelcome() //通过类来调用，不能通过实例调用
```

### 方法中的`self`属性

类的方法包含一个隐式的`self`属性。该属性用于指示目前的类实例。

```swift
class point {
    let x: Int
    let y: Int
    init (x: Int, y:Int) {
        self.x = x
        self.y = y
    }
}

var p = point(x:20, y:30)
print("x:\(p.x)")
print("y:\(p.y)")
```
