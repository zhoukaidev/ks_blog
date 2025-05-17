# 简介

前面介绍过了["操作符重载"之基本操作运算符的重载(operator op形式)](operatorOverload2.md)。

四种不同的操作符重载类型:

* `operator op`
* `operator type`
* `operator new / operator new[]`
* `operator delete / operator delete[]`
* `operator "" suffix-identifier`

本文会专注于介绍"`operator type`"类型的`用户自定义转换函数`。

## `operator type`类型函数签名

* `operator conversion-type-id`
* `explicit operator conversion-type-id`

上面的`conversion-type-id`代表不同的[type-id](https://en.cppreference.com/w/cpp/language/type#Type_naming)。

## 实例分析

分析一下`shared_ptr`中的`operator type`类型的函数:

```c++
#include <iostream>
#include <memory>

int main()
{
	using namespace std;
	shared_ptr<int> p1; // statement 1
	shared_ptr<int> p2 = make_shared<int>(1); // statement 2
	if (p1) {
		std::cout << "p1 store non-null pointer" << std::endl;
	}
	else {
		std::cout << "p1 store null pointer" << std::endl;
	}
	if (p2) {
		std::cout << "p2 store non-null pointer" << std::endl;
	}
	else {
		std::cout << "p2 store null pointer" << std::endl;
	}
	return 0;
}
```
在上述代码中:

1. 创建`p1`对象，内部包含一个空指针
2. 创建`p2`对象，内部包含一个int型指针

我们直接通过`if`语句来判断`p1, p2`是否包含空指针，并输出相应的字符串。

之所以可以直接通过`if`语句来判断`p1, p2`这两个`shared_ptr`对象是否包含空指针，是因为`shared_ptr`提供了相应的类型转换函数:

```c++
explicit operator bool() const noexcept;
```
上述的`if`语句可以转换为如下代码:

```c++
if(p1.operator bool()) {
    xxx
} else {
    xxx
}
if(p2.operatro bool()){
    xxx
}else {
    xxx
}
```

## 实战

创建一个三维点对象Point, 并提供函数判断是否为(0,0,0)点。

```c++
#include <iostream>
#include <memory>

class Point {
public:
	Point(int x, int y, int z) {
		mX = x;
		mY = y;
		mZ = z;
	}
    // 类型转换符，用于判断Point是否为(0, 0, 0)点
    // 对应于上述的`operator conversion-type-id`形式，这里的`conversion-type-id`为`bool`
	explicit operator bool() {
		if ((mX == 0) && (mY == 0) && (mZ == 0)) {
			return true;
		}
		return false;
	}
private:
	int mX;
	int mY;
	int mZ;
};

int main()
{
	Point p1(0, 0, 0);
	Point p2(1, 0, 0);
	if (p1) { 
		std::cout << "p1 is (0, 0, 0) point" << std::endl; 
	} else { 
		std::cout << "p1 is not (0, 0, 0) point" << std::endl; 
	}
	if (p2) { 
		std::cout << "p2 is (0, 0, 0) point" << std::endl; 
	} else { 
		std::cout << "p2 is not (0, 0, 0) point" << std::endl; 
	}
	return 0;
}
```

上面的代码为`Point`类实现了一个到`bool`类型的类型转换函数，用于判断Point包含的坐标点是否为(0, 0, 0);

上述代码的输出值为:

```c++
p1 is (0, 0, 0) point
p2 is not (0, 0, 0) point
```
