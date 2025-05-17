# 简介

本文主要介绍`python`中关于`全局变量`的使用方法。

`全局变量`是存在于整个程序生命周期的变量,所有的函数都可以访问这个全局变量。

## 定义全局变量

和定义函数类似，定义全局变量就是在全局空间中来声明定义一个变量。

```python
_globaVariable = "This is global variable"

# define myFun() method
def myFun():
  pass
```

## 访问全局变量

如果函数内部定义的局部变量的名称和全局变量的名称一致，该全局变量在函数内部会被隐藏。

### 读全局变量

```python
_globalVariable = "This is global variable"

def printVariable():
  print(_globalVariable)

if __name__ == "__main__":
  printVariable()
```

以上代码的输出值为:

>This is global variable

我们可以直接在函数内部访问`_globalVariable`全局变量。

### 写全局变量

在函数内部`写全局变量`的方法与`读全局变量`的方法略有不同,我会在后面的代码中演示这一点.

首先我们来看一个**错误**的案例:

```python
_globalVariable = "This is global variable"

def updateGlobalVariable():
  _globalVariable = "try to update _globalVariable in updateGlobalVarialbe method"
 
if __name__ =="__main__":
  print("Before update: ", _globalVariable)
  updateGlobalVariable()
  print("After update: ", _globalVariable)
```

以上代码的输出结果为:

> Before update:  This is global variable    
> After update:  This is global variable    

可以看出`_globalVariable`并没有按照预期的行为进行更新, 因为在`updateGlobalVariable`函数内部的
`_globalVariable = "try to update _globalVariable in updateGlobalVarialbe method"`语句被Python解释器理解为创建一个局部变量，这个局部变量
的名称为`_globalVariable`, 所以修改这个变量并没有影响外部的同名全局变量。

后面的代码会演示如何**正确**的修改该全局变量:

这里我们需要借助于`global`指示符,通过`global`指示符来告诉解释器,函数正在尝试修改的这个变量是一个外部的全局变量。

```python
_globalVariable = "This is global variable"

def updateGlobalVariable():
  global _globalVariable #通过global指示符来声明该全部变量
  _globalVariable = "try to update _globalVariable in updateGlobalVarialbe method"
 
if __name__ =="__main__":
  print("Before update: ", _globalVariable)
  updateGlobalVariable()
  print("After update: ", _globalVariable)
```

以上代码的运行结果为:

> Before update:  This is global variable    
> After update:  try to update _globalVariable in updateGlobalVarialbe method    
