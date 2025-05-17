## 简介

* 参考手册: [std::thread][thread]
* 头文件 "#include \<thread\>"
* [示例代码下载][sampleCode]
  
c++标准库中提供两种方法来创建线程，分别为`std::async`与`std::thread`,本章主要介绍`std::thread`的相关用法。

c++中通过`std::thread`类来创建一个新的线程，传入一个可调用的对象
或函数，同时传入函数所需要的相关参数。

## 示例

#### 创建线程

通过实例化`std::thread`并传入相关的可调用函数及所需的参数来创建一
个新的线程，当线程创建完成之后就**进入线程就绪队列等待运行**。

```cpp
void printValue(int j){
    std::cout << j << std::endl;
}

//创建一个线程 t,运行 printValue,并传入'3'作为参数
std::thread t(printValue, 3); 
```
#### 等待线程完成

在线程`t1`创建完成后，`t1`实例便和正在运行的线程绑定在一起，必须在合适的地方调用`std::thread::join()`来等待线程的完成或者调用`std::thread::detach()`来分离线程。

当函数`fun1`调用`std::thread::join()`后，会导致`fun1`阻塞，直到
线程完成并退出。

```cpp
//等待线程 t 完成并退出
t.join();
//或者分离线程
//t.detach();
```
#### 线程是否可以join

通过调用`std:thread::joinable()`来判断线程是否可以`join`或
`detach`.

```cpp
if (t.joinable()){
    t.join();
    //t.detach();
}
```

### thread中的异常

1. thread对象退出作用域时，要检测`joinable`的状态，在状态为`true`
的时候退出作用域会抛出异常

2. 当向`joinable`为`true`的`thread`对象赋值新的对象时，会导致
   抛出异常


[thread]:https://en.cppreference.com/w/cpp/header/thread
[sampleCode]: https://github.com/zhoukaisspu/blog_code/tree/master/standLibrary/thread