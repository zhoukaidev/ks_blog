## 简介

参考手册: [delegating constructor][delegatingConstructor]

委托构造函数就是在一个类的成员初始化列表中调用该类的其他构造函数。
针对委托构造函数，直接同时示例来展示时比较通俗易懂的。

## 示例

```cpp
class Foo{
public:
    Foo(int v1, int v2){
        m1 = v1;
        m2 = v2;
    }

    //在初始化列表中调用Foo(int v1, int v2)构造函数
    //此时m1 = a1; m2 = 0;
    Foo(int a1): Foo(a1, 0){

    }
private:
    int m1;
    int m2;
}
```

## 犯过的错误

```cpp
class ErrorFoo{
public:
    ErrorFoo(int v1, int v2){
        m1 = v1;
        m2 = v2;
    }
    /*此处并没有将ErrorFoo的构造委托给ErrorFoo(int v1,int v2),
    只是在构造函数内部创建了一个临时对象，所以调用该构造函数，
    会导致m1,m2并没有被正确的初始化*/

    ErrorFoo(int a1){
        ErrorFoo(a1, 0);
    }
private:
    int m1;
    int m2;
}
```

[delegatingConstructor]:https://en.cppreference.com/w/cpp/language/initializer_list#Delegating_constructor