### 简介

参考手册: [移动构造函数][moveConstructor]

类`T`的移动构造函数是指第一个参数为`T&&`,`const T&&`,`volatile T&&`或者`const volatile T&&`的构造函数，
于此同时没有其他参数或者其他参数全都有默认值。

### 声明语法

```cpp
class_name(class_name&&);
```

### 定义语法

```cpp
class_name : calss_name(class_name&& rvale)
{
    ...
}
```

### 使用条件

* 以`T`的右值初始化对象: T a = std::move(b);
* 向函数的参数传递一个右值: f(std::move(b));
* 返回值为存在移动构造函数的`T`,具体可以参考`RVO优化`

### 总结

1. 从参考手册上看到,移动构造函数允许形参为`const T&&`,但移动构造函数存在的意义为对象内部的内存搬移，所以实在想不到形参为常量的意义。



[moveConstructor]: https://en.cppreference.com/w/cpp/language/move_constructor