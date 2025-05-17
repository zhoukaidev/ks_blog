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
#include <iostream>

struct Foo {
    Foo() {
        i = 0;
        std::cout << "Foo constructor" << std::endl;
    }
    ~Foo() {
        std::cout << "Foo destructor" << std::endl;
    }
    int i;
};

struct Foo_2 {
    Foo_2() {
        i = 0;
        std::cout << "Foo_2 constructor" << std::endl;
    }
    ~Foo_2() {
        std::cout << "Foo_2 destructor" << std::endl;
    }
    int i;
};

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

int main()
{

    //fun_foo_2();
    //fun_foo();
    fun_foo();
    fun_foo_2();
    return 0;
}
```

#### static对象的析构顺序

观察以上代码的输出，会发现当函数调用相反的时候，输出的log也是
相反的，所以编译器是会创建相应的static对象初始链，在析构的时候，
会根据该初始化进行析构，最后初始化的static对象会最开始析构。
可以想象，在初始化时候，除了初始化该对象，还要把该对象指针放入
初始化链表中。以此来决定相应对象的析构顺序。

#### 实现该函数的伪代码

首先，static对象只会在第一次函数调用的时候初始化该对象，所以
首先需要相应的标识符来标识该对象是否已经被初始化，其次将已经
初始化的对象的地址放入相应的链表中来记录初始化顺序。

```cpp
int fun_foo()
{
    static Foo s_foo;
    s_foo.i++;
    return s_foo.i;
}

//伪码
bool s_foo_init = false;
int fun_foo()
{
    static Foo s_foo;
    if(!s_foo_init){ // 第一次调用该函数
        enter_thread_guard; // 进入线程安全
        Foo::Foo(&s_foo); // 初始化s_foo;
        s_foo_init = true; // 标记已经初始化
        link_list.push(&s_foo); // 该对象地址放入链表中
        exit_thread_guard; // 退出线程安全
    }
    s_foo.i++;
    return s_foo.i;
}

```

从上面的伪代码中，我们可以看到在实现相应的static对象可以采用
的模型，以此来满足static对象的各种要求。