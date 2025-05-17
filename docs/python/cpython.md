# 简介

本文主要介绍有关`CPython`解释器的相关参数及使用方法。

[CPython](https://github.com/python/cpython)解释器是一个开源的工程，业余时间也可以去研究该解释器的具体实现。

## 参数

CPython和其他各种日常使用的程序一样，也会支持不同种类的参数来执行不同的行为。

```py
python [-bBdEhiIOqsSuvVWx?] [-c command | -m module-name | script | - ] [args]
```
* **-c \<command\>**

使用python解释器来执行"<command>"

```py
python -c "print('hello world')"
```

* **-m \<module-name\>**

通过`sys.path`路径寻找该"module",并作为"__main__"模块来执行该内容。

```py
python -m venv ll_env
```
