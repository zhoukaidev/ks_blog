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

[nativeHandle]:https://en.cppreference.com/w/cpp/thread/thread/native_handle