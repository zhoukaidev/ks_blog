## 简介

**单例模式**是很常用的一种设计模式，在实现过程中要非常注意线程安全，
我们会介绍四种方式来实现线程安全的单例模式:

* std::mutex实现单例模式
* std::call_once实现单例模式
* 借助static member实现单例模式
* 使用std::atomic来实现double check 模式
  
本文会介绍前两种实现方法，后面两种实现方法请参考[本文](singleTon_atomic_static_member.md).

## 实现方法

### 借助std::mutex

```cpp
class SingleTon {
public:
    static SingleTon* getInstance(void)
    {
        std::lock_guard<std::mutex> lk(s_mtx);
        if (s_p == nullptr) {
            s_p = new SingleTon();
        }
        return s_p;
    }
public:
    int getValue() {
        return m_int;
    }
private:
    static std::mutex s_mtx;
    static SingleTon* s_p;
    SingleTon(SingleTon&) = delete;
    SingleTon& operator=(SingleTon&) = delete;
    SingleTon(SingleTon&&) = delete;
    SingleTon& operator=(SingleTon&&) = delete;
    SingleTon() {
        m_int = 0;
    }
private:
    int m_int;
};
```

上面的实现中，可以保证在多线程环境下调用`getInstance`
是安全的，但在每次调用该函数的时候，都要求获取`mutex`,
这会降低该函数的性能。

基于以上的代码，我们在来做一些修改，看一下其中会存在什么样的问题。

```cpp
static SingleTon* getInstance(void)
{
    if(s_p == nullptr){
        std::lock_guard<std::mutex> lk(s_mtx);
        if(s_p == nullptr){
            s_p = new SingleTon();
        }
    }
    return s_p;
}
```
在解释上面的修改之前，我们先记住两个概念，编译器的指令优化会将部分指令打乱，其次
是CPU也会乱序执行，这使得很多指令并不像我们想象中的顺序那样运行。这使得上面的代码
**不是线程安全的**.

`s_p = new SingleTon();`这句代码包括三个部分:

    1. 申请内存空间
    2. 调用构造函数初始化内存空间
    3. 将地址指针赋值给`s_p`

在实际运行过程中，编译器或CPU会执行某些优化，很有可能使得指令运行顺序变成**1,3,2**,
如果在执行完`1,3`之后，线程被切换，这时候问题出现了，其他线程很有可能获得该指针，但该指针所指向的地址空间并没有来得及进行初始化。

### 借助std::call_once与std::once_flag

在c++中可以提供一个可调用对象(fn)给`std::call_once`,该函数
可以确保fn只被调用一次。

```cpp
class SingleTon {
public:
    static SingleTon* getInstance(void)
    {
        std::call_once(s_flag,initSingleTon);
        return s_p;
    }
public:
    int getValue() {
        return m_int;
    }
private:
    static SingleTon* s_p;
    static std::once_flag s_flag;
    static void ininSingleTon() {
        s_p = new SingleTon();
    }
    SingleTon(SingleTon&) = delete;
    SingleTon& operator=(SingleTon&) = delete;
    SingleTon(SingleTon&&) = delete;
    SingleTon& operator=(SingleTon&&) = delete;
    SingleTon() {
        m_int = 0;
    }
private:
    int m_int;
};
```
