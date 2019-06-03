## 函数简介 #

函数是用于执行特定任务的一系列的指令集。
* 函数声明: 向编译器提供函数名称，返回值及参数
* 函数定义: 函数的具体实现

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

