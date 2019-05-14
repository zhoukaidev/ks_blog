### 简介

c++默认构造函数(Default constructor)是指*不传入任何参数便可
以调用*的构造函数，这意味着构造函数可以是**没有任何参数**的构
造函数或者是**每个参数都有默认值**的构造函数。

### 语法

* 声明语法

```
Classname();
//这里的"int a = 0"可以替换成其他任何类型的默认参数
Classname(int a = 0); 
```

* 定义语法

```
Classname::Classname(){...}
Classname::Classname(int a = 0){...}
```

### 总结

> 当在一个类中存在多个默认构造函数的时候，需要如何处理?

```cpp
class Foo {
public:
    Foo() // default constructor
    { 
        std::cout << "defautl constructor" 
            << std::endl;
    }

    // has default parameter 
    Foo(int i = 0) // default constructor 
    {
        std::cout << "Foo second constructor: " 
            << i << std::endl;
    }
};
```

针对`Foo`类的情况，在创建对象时需要显式的说明使用哪一个构造函数。   
例如：
```cpp
Foo f1();
Foo f2(3);
//Foo f3; //'Foo::Foo' ambigious to overload function
```