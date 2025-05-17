## 简介

参考: [std::thread::native_handle()][nativeHandle]

c++中的线程库`std::thread`所提供的线程控制能力非常有限，
线程创建完成后即开始运行，只提供了`joinable`,`join`,`detach`，
为了弥补这个不足，c++提供了一个`std::thread::native_handle()`
函数来**获取与特性线程库实现相关的`handle`**,以此来提供更多线程控制能力。

## 接口

```cpp
native_handle_type native_handle();
```

## 例程

假设目前存在线程A与B，如果希望通过线程B来挂起线程A,目前通过C++标准库提供的接口并
无法实现这个功能，这时候我们需要通过`native_handle()`来返回与操作系统相关的`HANDLE`,
然后调用操作系统提供的线程操作接口来实现这个功能。

在本例程中调用`SuspendThread(...)`来挂起线程，调用`ResumeThread(...)`来恢复线程执行。


```c++
//Platform: win10
//IDE: vs2017
#include <chrono>
#include <thread>
#include <iostream>
#include <windows.h>

void printHello()
{
	int i = 0;
	while (true) {
		std::this_thread::sleep_for(std::chrono::seconds(1));
		std::cout << i << " :" << "Hello world" << std::endl;
		++i;
	}
}
int main()
{
	std::thread th(printHello);
	SuspendThread(th.native_handle()); //挂起th线程
	std::cout << "Suspend printHello thread" << std::endl;
	for (int i = 0; i < 3; ++i) {
		std::this_thread::sleep_for(std::chrono::seconds(1));
		std::cout << "main thread sleep " << (i + 1) << " s" << std::endl;
	}
	std::cout << "Resume printHello thread" << std::endl;
	ResumeThread(th.native_handle()); // 3s后恢复th线程
	while(1){ }
    return 0;
}
// 可能输出
// Suspend printHello thread
// main thread sleep 1 s
// main thread sleep 2 s
// main thread sleep 3 s
// 0 :Hello world
// ...
```


[nativeHandle]:https://en.cppreference.com/w/cpp/thread/thread/native_handle