# 简介

本文主要介绍与`python`相关的工具及如何进入`python`的世界。

## 基础结构

![PythonOverview](./asset/pythonOverview.PNG)

## 安装pip

`pip`为python所使用的安装包管理工具，大部分的`第三方开发包`都是借助`pip`进行安装。

以下介绍如何在各个平台上安装`pip`:

* ubuntu
    * 安装python3的pip: `sudo apt-get install python3-pip`
    * 安装python的pip: `sudo apt-get install python-pip`
    
* 为pip设置代理
   通过指定`proxy`参数来设置代理
   ```sh
   pip install --proxy=http://web-proxy.us.xxxx:8080 Django
   ```

## 参考手册

* [install pip on ubuntu](https://linuxize.com/post/how-to-install-pip-on-ubuntu-18.04/)
* [python3 standard Library](https://pymotw.com/3/index.html)

## 学习资源

* [PyMOTW3: Python3 standard library by example](https://pymotw.com/3/index.html)

### coroutines

* [The basic of genertors](https://realpython.com/introduction-to-python-generators/)
