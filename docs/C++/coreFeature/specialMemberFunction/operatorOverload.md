# 操作符重载

`操作符的重载`是在实际的`C++`编程过程中不太容易引人注意但却非常实用的一个特性。   
合理的实现`操作符重载`可以极大的提高编程体验，但是不合理的实现也可能会在使用过程中给开发人员
带来很大的困惑。

本篇文章会首先分析一些`c++`标准库中所实现的一些`操作符重载`, 然后在具体介绍如何实现操作符重载。

本文后续主要会分析如下操作符:

* std::string 中对`[]`及`+=`操作符重载
* std::shared_ptr中对`*`及`->`操作符重载

## std::string中的操作符

```c++
#include <string>
#include <iostream>
int main()
{
	std::string str = "Hello ";
	str += "World";
	for (auto i = 0; i < str.length(); ++i) {
		std::cout << str[i] << std::endl;
	}
	return 0;
}
```

体会以下上面的代码，很简单而且很直观，

1. `std::string str = "Hello "` 定义了一个`string`对象，且初始值为`Hello `
2. `str += "World"`往`str`里添加新的字符，此时str的内容变为`Hello World`
3. 通过`for`循环,以`str[i]`的形式访问str里的每一个字符

通过 `+=` 的形式来对`string`对象添加内容, 通过`[]`的形式访问`string`对象内的每一个字符，使得对于`string`对象
的使用很自然，但这背后其实是`string`类对`+=` 操作符及 `[]` 操作符进行了重载。

来看一下[`string`头文件](https://en.cppreference.com/w/cpp/string/basic_string)中操作符重载的形式:

```c++
// []操作符重载
char&       operator[]( size_type pos );
const char& operator[]( size_type pos ) const;

// "+="操作符重载
basic_string& operator+=( const basic_string& str );
...(详细可以参考cppreference)
```

`string`类中对这些操作符进行了重载, 当使用这些操作符的时候,实际上是在调用以上的这些函数,使得对于`string`对象的使用自然，直接。

## std::shared_ptr中的操作符

```c++
#include <iostream>
#include <memory>
#include <vector>

int main()
{
	using namespace std;
	shared_ptr<vector<int>> ptr = make_shared<vector<int>>();

	ptr->push_back(1);
	(*ptr).push_back(2);
	
	for (auto i = 0; i < ptr->size(); ++i) {
		std::cout << (*ptr)[i] << std::endl;
	}
	return 0;
}
```

1. ptr为`shared_ptr<vecotr<int>>`类型对象，ptr内部管理的是`vector<int>`类型的指针
2. `ptr->push_back(1)`的使用是不是感觉`ptr`是一个`vector<int>`类型的指针，并不是所谓的`shared_ptr`对象
3. `(*ptr).push_back(2)`的使用是不是也感觉`ptr`就是`vector<int>`类型的指针

!!! note
        以上的`ptr`是个`shared_ptr`类型对象，内部包含一个指针

对`ptr`如此直接自然的使用，背后其实也是`操作符重载`在捣鬼。

看一下`shared_ptr`中对`*`及 `->`操作符的重载:

```c++
// 对 "*" 的重载
T& operator*() const noexcept;
// 对 "->" 的重载
T* operator->() const noexcept;
```

* `ptr->push_back(1)`的背后是调用了重载的`->`操作符:

```c++
(ptr.operator->())->push_back(1);
```

* `(*ptr).push_back(2)`是调用了重载的`*`操作符:

```c++
(ptr.operatro*()).push_back(2);
```

看似简单直接的调用实际上背后却发生了很多的事情，不容易发现，但确实在发生，这就是操作符重载的魅力。

## 总结

大概介绍了一些标准库中使用的`操作符重载`，让我们有了一个直观的感受，后面几篇文章会详细介绍如何来实现操作符重载。
