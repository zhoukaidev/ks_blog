## 简介

swift一门强类型语言,意味着当一个变量类型确定后，不能够将其他类型的变量直接赋值给该变量。


## 内置数据类型

* Int or UInt
   * Int32,Int64,UInt32,UInt64
* Float
   * represent a 32 bit floating-point number
* Double
   * represent a 64-bit floating-point number
* Bool
* String
* Character
* Optional
   * represents a variable that can hold either a value or no value
* Tuples

## 数据类型特征

* 类型安全

swift在进行代码编译时，会执行类型检查步骤。

* 类型推断

## 变量声明与定义

* 使用`var`关键字声明变量

```swift
var varA = 43
print(varA)
```
* 强制类型指定

```swift
var varB:Float;
varB = 2.343;
print(varB);
```

* `Optionals`类型 与 `nil`关键字
   * 强制类型展开
   * 自动类型展开
   * 自动绑定

```swift
var perhapsInt: Int? //optional Integer declaration
var perhapsString: String? //optional string declaration
var perhapsString2: String? = nil; // use nil to initialize the perhapsString2

var myString:String!  // automatic unwrapping optionals
```
强制类型展开:

```swift
var myString:String?
myString = "Hello ,swift"
if myString != nil {
    print(myString!) // forced unwrapping 
} else {
    print("myString has nil value")
}
```
自动类型展开:

```swift
var myString:String!
myString = "Hello , swift 4"
if myString != nil {
    print(myString)
} else {
    print("myString has nil value")
}
```
* `Tuples`类型
   * 可以包含任何数据类型
   * 使用`()`符号来定义`Tuples`类型数据

```swift
var myTuple = (24, "Joe", "Student", 34.3) // contains Integer,string and float
```
* `let`关键字声明常量
   * 声明常量
   * 常量类型声明

```swift
let constA = 42 // constant interger has a value 42
let constB:Float = 3.14159 // type annotations with constB

```

* `Arrays`类型
   * 创建数组
   * 访问内部数据
   * 修改数组
   * 迭代数组

swift4的数组用于存储相同类型的有序数据列表。

创建数组：

```swift
var array1 = [Int]()  // creat empyt array
var array2 = [Int](repeating: 0, count: 3) // create an array of a given sie and initialize it with default value
var array3:[Int] = [10, 20, 30] // create an array of three elements
```

访问内部数据:
```swift
var someInts = [10, 20, 30]
var index_1 = someInts[0]
print(index_1)
```
* `Sets`数据类型
   * 创建`Sets`
   * 访问及修改`Sets`

创建`Sets`:
```swift
var someSet = Set<Character>() // Character can be replaced by data type of set.
```



