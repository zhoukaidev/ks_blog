## 类的属性分类

* stored property
* lazy stored property
* computed property 
* Type property

## 类属性介绍

* stored property

`stored property`用于存储相应的常量或变量实例。

常量使用`let`关键字定义,变量使用`var`进行定义。

```swift
class person {
    let name:String // stored property
    init (name:String) {
        self.name = name
    }
}
```

* lazy stored property
