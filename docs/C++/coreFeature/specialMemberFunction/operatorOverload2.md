# 简介

在[上篇文章](operatorOverload.md)中，我们应该可以直观感受到什么是操作符重载。

现在我们要正式进入到理论学习中:

* 什么是操作符重载
* 不同类型的操作符重载及语法
* 如何实现操作符重载

本文为阅读[cppreference operator overloading 章节](https://en.cppreference.com/w/cpp/language/operators)的总结。

## 什么是操作符重载

`被重载的操作符`实际上就是一些具有特殊函数名称的函数。

## 不同类型的操作符重载

截止到`C++17`,共有五种不同类型的操作符重载，语法如下:

* `operator op`
* `operator type`
* `operator new / operator new[]`
* `operator delete / operator delete[]`
* `operator "" suffix-identifier`

本文主要介绍第一种`operator op`类型的重载，后面几种类型会在后面的文章中进行介绍。

!!! note
    `op`包括如下操作符:
    "`+`"  "`-`"  "`*`"  "`/`"  "`%`"  "`^`"  "`&`" "`|`" "`~`"  "`!`"    
    "`=`"  "`<`"  "`>`"  "`+=`"  "`-=`" "`*=`" "`/=`"  "`%=`" "`^=`"    
    "`&=`" "`|=`"  "`<<`"  "`>>`" "`>>=`"  "`<<=`"  "`==`" "`!=`" "`<=`"
    "`>=`" "`&&`"  "`||`"  "`++`" "`--`"  "`,`" "`->*`"    
    "`->`"  "`( )`"  "`[ ]`"

### 实现操作符重载

`操作符重载`并不是没有任何限制，在重载操作符的时候， 不同操作符的函数签名如下所示:

| 表达式  | 作为成员函数  | 作为非成员函数  | 例程  |
|--------|---------------|---------------|-------|
| `@a`   | `(a).operator@()` | `operator@(b)` | !std::cin 调用 std::cin.operator!() |
| `a@b`  | `(a).operator@(b)` | `operator@(a, b)` | std::cout << 42 调用 std::cout.operator<<(42)>> |
| `a=b`  | `(a).operator=(b)` | 不能作为非成员函数 |  std::string s; s = "abc" 调用 s.operator=("abc") |
| `a(b...)` | `(a).operator()(b...)` | 不能作为非成员函数 |  -- |
| `a[b]`  | `(a).operator[](b)` | 不能作为非成员函数 | std::string m("hello"); m[0] = 's';调用 m.operator[](0) = 's' |
| `a->` | `(a).operator->()` | 不能作为非成员函数 | auto p = std::make_unique<S>(); p->bar() 调用 p.operator->() |
| `a@` | `(a).operator@(0)` | `operator@(a, 0)` | std::vecotr<int>::iteraotr i = v.begin(); i++ 调用 i.operator++(0) |
| **表格中的`@`符号为占位符，代表所有符合要求的操作符**  | -| -| - |

### 实战

我们来实现一个简单的三维坐标类，并重载部分的操作符:

```c++
#include <iostream>
#include <memory>
#include <vector>
#include <string>

class Point {
public:
	Point(int x = 0, int y = 0, int z = 0) {
		mX = x;
		mY = y;
		mZ = z;
	}
    // 重载`=`操作符，对应于上表中的`a=b`
	Point& operator=(int value) {
		mX = value;
		mY = value;
		mZ = value;
		return *this;
	}
    // 重载`[]`操作符，对应于上表中的`a[b]`
	int& operator[](char name) {
		if (name == 'x') return mX;
		else if (name == 'y') return mY;
		else return mZ;
	}
    // 重载`++`操作符，对应于上表中的`a@`
	Point& operator++(int) {
		mX++;
		mY++;
		mZ++;
		return *this;
	}
	std::string value() {
		return "X=" + std::to_string(mX) 
				+ "; Y = " + std::to_string(mY)
				+ "; Z = " + std::to_string(mZ);
	}
private:
	int mX;
	int mY;
	int mZ;

};

int main()
{
	Point p;
	std::cout << p.value() << std::endl;
	p++; // 调用p.operator++();
	std::cout << p.value() << std::endl;
	std::cout << "value x=" << p['x'] << std::endl; // 调用p.operator[]('x')
	std::cout << "value y=" << p['y'] << std::endl; // 调用p.operator[]('y')
	std::cout << "value z=" << p['z'] << std::endl; // 调用p.operator[]('z')
	return 0;
}
```

输出值为:
```
X=0; Y = 0; Z = 0
X=1; Y = 1; Z = 1
value x=1
value y=1
value z=1
```

## 后续

后面的文章在介绍其他类型的操作符重载。