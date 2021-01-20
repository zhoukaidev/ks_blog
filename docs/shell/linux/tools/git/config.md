# 简介

本文主要介绍如何对`git`进行各种不同类型的配置。

* 配置`username`和`email`


## 配置`username`和`email`

这里有两种不同类型的`username`和`email`的配置:

* 为本机上所有的仓库配置`username`和`email`

```sh
//配置全局username
git config --global user.name "myName"
//配置全局email
git config --global user.email "myEmail"
```

* 为单独仓库配置`username`和`email`

```sh
// 1. 切换到仓库目录下
// 2. 配置针对该仓库的username
git config user.name "myName"
// 3. 配置针对该仓库的email
git config user.email "myEmail"
```

## 配置编辑器

```sh
git config --global core.editor "vim"
```

## 配置代理

```sh
git config --global http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port
```
