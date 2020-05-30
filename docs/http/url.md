# 简介

本文主要用于介绍构成`URL`的基本组件。

`URL`是`Uniform Resource Locator`的缩写,是在`HTTP`协议中一个非常重要的组件。`HTTP`协议使用`URL`来定位
网络世界中的唯一资源。

理解`URL`组件的不同模块能够帮助我们更好的理解`HTTP`.

> 注: 该文主要是阅读https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL 的个人总结。
> 所以大部分内容也是摘自该处。

## URL基本形式

我们主要分析下面这个`URL`的构成模块:

* `http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument`
