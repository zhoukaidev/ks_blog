## subscripts简介

不知道`subscripts`应该翻译成什么比较合适，所以在这里就使用`subscripts`,而不使用对应的中文。

*subscripts*实际上是类访问列表,集合或序列的一种快捷方式。

你可以通过*subscripts*来访问或修改数据。例如我们可以通过somaArray[index]的形式来访问一个Array中的某一个元素。Subscripts不仅可以是一维的，我们可以根据需求定义多维的输入。

对于熟悉C++的人而言，这里的subscripts实际上就是"[ ]操作符重载"。

以下内容分为:

* subscript语法
* 定义read-only的subscript
* 定义read-write的subscript
* Type subscripts

## subscript语法

通过使用`subscript`关键字,然后紧接着指定一个或多个输入参数及返回类型来定义subscript.

```swift
subscript(index: Int) -> Int {
    get {
        // 返回相应的值
    }
    //这里newValue的类型与设定的返回值类型相同
    set(newValue) {
        //设置新的值
    }
}
```

## 定义read-only的subscript

通过移除上面指定的`get`与`set`便可以实现read-only的subscript.

* read-only的subscript语法

```swift
subscript(index: Int) -> Int {
    //根据index返回相应的值
    //此时subscript为read-only
}
```

* read-only的subscript例子

```swift
// 例程来自: https://docs.swift.org/swift-book/LanguageGuide/Subscripts.html
struct TimesTable {
    let multiplier : Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}

let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is: \(threeTimesTable[6])")
//输出: "six times three is 18"
```

## 定义read-write的subscript

当需要定义`read-write`形式的subscript时，就需要使用前面提供的`get-set`形式的subscript.

* read-write的subscript例子

```swift
class welcomeString {
    var welcome = ["hello", "hi", "nice"]
    subscript(index: Int) -> string {
        get {
            return welcome[index]
        }
        set(newValue) {
            self.welcome[index] = newValue
        }
    }
}
var wel = welcomeString()
print(wel[0])  // read by subscript
wel[0] = "change welcome string" // write by subscript
print(wel[0])
```

## Type subscripts

TODO