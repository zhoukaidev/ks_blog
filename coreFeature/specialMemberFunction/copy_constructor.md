### 简介

参考手册: [copy constructor][copy_constructor]

类`T`的拷贝构造函数是指第一个参数为`T&`,`const T&`,`volatile T&`或`const volatile T&`,与此同时不存在其他参数，或者其他参数均有默认值。

### 声明语法

```cpp
class_name(const& class_name);
```

### 定义语法

```cpp
class_name : class_name(const& class_name)
{
    ...
}
```

### 使用方式

以下三种方式都会调用`T`的拷贝构造函数:

* 直接初始化: T a = b; T a2(b);
* 函数参数传递: void f(T a);
* 函数返回值: 在T不支持移动构造函数的时候,在函数f中返回T的对象

```cpp
class_name b; // use default constructor
class_name a(b); // use copy constructor
class_name a = b; // use copy constructor
```

[copy_constructor]:https://en.cppreference.com/w/cpp/language/copy_constructor