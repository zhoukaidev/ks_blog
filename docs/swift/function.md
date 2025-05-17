## 函数简介 #

函数是用于执行特定任务的一系列的指令集。

* 函数声明: 向编译器提供函数名称，返回值及参数
* 函数定义: 函数的具体实现

这里主要分为两种不同的函数类型:

* 全局函数(global function)
* 嵌套函数(nested function)
  
## 函数定义

* 使用`func`关键字定义函数

函数定义语法:
```swift
func funcname(Parameters) -> returnType {
    statement1
    statement2
    ...
    return parameters
}
```

函数定义例程:

```swift
// 函数名称: student
// 函数返回类型: String
// 函数参数: 
//          name: 字符串类型
func student(name: String) -> String {
    return name;
}
print(student(name:"First function"))
print(student(name:"Second function"))
```

## 函数参数与返回值

* 有参数函数
* 无参数函数
* 有返回值函数
* 无返回值函数
* `Optional`类型的返回值

```swift
//有参数的函数
func mult(no1: Int, no2: Int) -> Int {
    return no1 * no2;
}

// 无参数的函数
func name() -> String {
    return "Bob"
}

// 有返回值的函数
func add (a: Int, b: Int) -> Int {
    return a + b;
}

// 无返回值的参数
func sum (a: Int, b: Int) {
    let a = a + b
    let b = a - b
    print(a, b)
}
// 返回值类型为Optioal
func minMax (array: [Int]) -> (min:Int, max: Int)? {
    if array.isEmpty {return nil}
    var currentMin = array[0]
    var currentMax = array[0]
    return (currentMin, currentMax)
}
```

## 本地及外部参数名称

* 本地参数名称

```swift
func sample(number: Int) {
    print(sample)
}
sample(number: 1)
sample(number: 2)
```

* 外部参数名称

外部参数名称允许重新命名参数的名称，使得参数的名称表达的更加清晰。
比如为了表达参数的意义，可能需要很长的字符串，这样会导致内部实现中多次出现这些参数名称，使得
内部实现不简洁，这是外部参数名称便解决了这个问题。

```swift
//不使用外部参数名称
func getName (firstName: String, middleName: String, lastName: String) {
    let name = firstName + middleName + lastName
    print(name)
}
getName(firstName:"first", middleName:"middle", lastName:"last")
//使用外部参数名称
func getName2 (firstName a:String, middleName b:String, lastName c:String) {
    let name = a + b + c
    print(name)
}
getName(firstName:"first", middleName:"middle", lastName:"last")
```
## 函数类型

* 定义函数类型
* 函数类型作为参数类型
* 函数类型作为函数返回值

定义函数类型:

```swift
func sum (a: Int, b: Int) ->Int {
    return a + b
}
var addition: (Int, Int) -> Int = sum //定义addition类型为sum的函数类型
print(addition(a: 2, b: 3)) // 调用addition函数
```

函数类型作为参数类型:

```swift
func sum (a: Int, b: Int) -> Int {
    return a + b
}

func funcWrapper(addition: (Int, Int) -> Int, a: Int, b: Int) {
    let res = addition(a, b)
    print(res)
}

var add: (Int, Int) -> Int = sum
funcWrapper(addition: add, a: 10, b: 30)
```

函数类型作为返回值/嵌套函数:

```swift
//返回类型为()->Int
func calcAdd(a: Int, b: Int) -> () -> Int {
    var initer  = 10
    func add() -> Int {
        return a + b + initer
    }
    return add
}
let add = calcAdd(a: 3, b: 4)
print(add())
```
