## 简介

本文主要介绍C++11之后关于函数内部static对象(scoped static)的
相关构造与析构模型。

>Note: 本文章大部分内容为阅读《c++对象模型》的总结。

本文尝试解释两个问题:

  1. c++如何构造scoped static对象
  2. c++采用何种规则析构scoped static对象
 
 ### 前言

 在学习scoped static对象的过程中，我们会经常听到这些结论:

 * 该对象放置在全局数据段中
 * 该对象只会在第一次调用该函数的时候被初始化
 * 该对象的作用域为函数内部
 * 该对象的生命周期和应用生命周期相同
 * 该对象的初始化为线程安全的
  
### 编译器如何实现上述功能

示例代码:

```cpp
struct Foo {
    Foo() {
        i = 0;
        std::cout << "Foo constructor" << std::endl;
    }
    ~Foo() {
        std::cout<<"Foo destructor" << std::endl;
    }
    int i;
}

struct Foo_2 {
    Foo_2() {
        i = 0;
        std::cout << "Foo_2 constructor" << std::endl;
    }
    ~Foo_2() {
        std::cout<<"Foo_2 destructor" << std::endl;
    }
    int i;
}

int fun_foo()
{
    static Foo s_foo;
    s_foo.i++;
    return s_foo.i;
}

int fun_foo_2()
{
    static Foo_2 s_foo_2;
    s_foo_2.i++;
    return s_foo_2.i;
}
```
