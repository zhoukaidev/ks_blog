
* c++博客的写作要求
* c++核心语言特性(core feature)
    * [c++构造函数][constructor]
    * c++析构函数
    * "default" and "delete"
    * "virtual" and "override"
* c++标准库
    * c++多线程
        * [std::thread][thread]
        * [std::thread::native_handle][threadNativeHandle]
        * 互斥量
            * [mutex & shared_mutex][mutexSharedMutex]
            * timed_mutex & recursive_mutex 
* c++对象模型
    * static对象的构造与析构
        * [函数内部static对象构造与析构][scopedStatic]
        * 全局static对象构造与析构 
* c++内容杂谈
    * [c++委托构造函数(Delegating constructor)][delegatingConstructor]
    * 线程安全的单例模式(signton pattern) 
        * [借助std::mutex或std::call_once实现][singleton_pattern_call_once]
        * [借助double check或static member实现][singleton_atomic_static_member]
    



[thread]:./standardLibrary/multiThread/thread.md
[constructor]:./coreFeature/specialMemberFunction/constructor.md
[threadNativeHandle]:./standardLibrary/multiThread/thread_nativeHandle.md
[mutexSharedMutex]:./standardLibrary/multiThread/mutex_shared_mutex.md
[delegatingConstructor]:./coreFeature/specialMemberFunction/delegating_constructor.md
[singleton_pattern_call_once]:./others/singleTon_mutex_call_once.md
[singleton_atomic_static_member]:./others/singleTon_atomic_static_member.md

[scopedStatic]:./objectModel/scoped_static.md

