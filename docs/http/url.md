# 简介

本文主要用于介绍构成`URL`的基本组件。

`URL`是`Uniform Resource Locator`的缩写,是在`HTTP`协议中一个非常重要的组件。`HTTP`协议使用`URL`来定位
网络世界中的唯一资源。

理解`URL`组件的不同模块能够帮助我们更好的理解`HTTP`.

> 注: 该文主要是阅读 [https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL) 的个人总结。
> 所以大部分内容也是摘自该处。

## URL基本形式

我们主要分析下面这个`URL`的构成模块:

* `http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument`

1. `http`:代表采用的是**http**通讯协议
2. `www.example.com`为域名，经过DNS解析后,会得到对应的IP地址。
3. `80`: 为服务的端口号
4. `/path/to/myfile.html`指向服务器的资源地址。类似于某个物理文件在服务器上的路径
5. `?key1=value1&key2=value2`是一系列提供给服务器的额外参数,采用key/value对的形式,其中`?`为分隔符,分隔符后的为参数对。服务器可以通过这些额外参数来进行一些额外的处理,生成针对性的资源返回给用户.
6. `#SomewhereInTheDocument` 代表某个资源文件内部的一个书签,浏览器可以通过该书签自动滑动页面,使得该书签所指向的内容居于浏览器显示区域中间。该标识符不会发送给服务器端。

## 参考文档

* [What is a URL?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)
