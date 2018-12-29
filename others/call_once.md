## 简介

**单例模式**是很常用的一种设计模式，存在很多种在单线程环境下实现
单例模式的方法，本文主要会介绍四种方法，其中包括名声不怎好的
`double check`实现方法。

* std::mutex实现单例模式
* std::call_once实现单例模式
* 借助static member实现单例模式
* 使用double check 模式
  
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

### 借助std::call_once与std::once_flag

在c++中可以提供一个可调用对象(fn)给`std::call_once`,该函数
可以确保fn只被调用一次。
