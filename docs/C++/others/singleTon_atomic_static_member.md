## 简介

本文介绍**单例模式**实现的另外两种方法:

* 通过double check(借助std::atomic)实现单例模式
* 采用static member实现单例模式

### double check实现单例模式

在使用double check来实现线程安全的单例模式中，我们需要使用`std::atomic`
来实现必要的同步。

```cpp
class SingleTon {
public:
    static SingleTon* getInstance(void)
    {
        if(s_p.load() == nullptr){
            std::lock_gurad<std::mutex> lk(s_mtx);
            if(s_p.load() == nullptr){
                auto p = new SingleTon();
                s_p.store(p);
            }
        }
        return s_p.load();
    }
public:
    int getValue() {
        return m_int;
    }
private:
    static std::mutex s_mtx;
    static std::atomic<SingleTon*> s_p;
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

### 借助static member实现单例模式

在c++11中，c++标准开始支持多线程模式，函数内部的静态成员变量的初始化为线程安全的，
这也很大的简化了单例模式的实现方始。

```cpp
class SingleTon {
public:
    static SingleTon& getInstance(void)
    {
        static SingleTon s_singleTon(); //采用静态成员变量
        return s_singleTon;
    }
public:
    int getValue() {
        return m_int;
    }
private:
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