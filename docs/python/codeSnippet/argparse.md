# 简介

本文主要介绍`python`中`argparse`模块的主要用法。

在日常编程过程中,我们需要通过不同的命令行参数来为我们的程序指定不同的行为。 这就涉及到该如何解析用户传递的命令行参数。

`argparse`模块就是用来帮助我们进行命令行参数的处理的。

## 参数类型

`argparse`模块包含两种不同类型的参数:

* 位置参数
* 可选参数

### 位置参数

`位置参数`是指参数与参数传入位置有关的那些参数，**通常**位置参数也是必须传入参数，否则会导致程序无法正常运行。

假设有一个程序用于将文档中所有的小写字母修改为大写字母，该程序需要两个参数, 输入文件的位置及输出文件的位置，我们可以采用
如下方式来定义该命令行参数:

```py
import argparse

parser = argparse.ArgumentParser(description="Convert little case to upper case")
parser.add_argument('indir', type=str, help="path of input file")
parser.add_argument('outdir', type=str, help="path of output file")
args = parser.parse_args()
print(args.indir)
print(args.outdir)
```
在以上的程序中， 我们分别定义了 `indir` 和 `outdir` 为输入路径及输出路径，在经过`parse.parse_args()`之后，我们可以从`args`对象中分别
取出`indir`和`outidr`的值。

> Note: 这里我们调用`add_argument`函数的时候，`indir`和`outdir`前面并没有添加`-`符号，如果添加了该符号，则代表该参数类型
> 为可选参数了。



## 参考文档

* [learn enough python to be useful-argprse](https://towardsdatascience.com/learn-enough-python-to-be-useful-argparse-e482e1764e05)
* [argparse in PYMOTW](https://pymotw.com/3/argparse/index.html)
