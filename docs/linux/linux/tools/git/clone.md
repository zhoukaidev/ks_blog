# 简介

`git clone` 是用于从远端代码服务器(比如[github](www.github.com))下载远端仓库的基本指令。


## 基本用法

*  `git clone url_of_remote_reporsitory`

如果我需要下载https://github.com/zhoukaisspu/testing.git,则可以使用以下指令:

```sh
git clone https://github.com/zhoukaisspu/testing.git
```

### shallow-clone

在某些情况下,我们的代码仓库可能因为多次的提交,导致仓库很大,每次`clone`会花费很长的时间及磁盘空间,这里
我们可以使用`shallow-clone`的方式，仅`clone`最新的提交, 而不是把每次的提交历史都`clone`下来,以此来提升`clone`的性能。

* `git clone [-b <branchName>] repository_url [--depth <depth>]`

在上面的指令中我们通过:

1. `[-b <branchName>] 指定仅clone某个分支`
2. `[--depth <depth>] 指定仅clone指定数量的commits`

如果我需要从https://github.com/zhoukaisspu/testing.git下载`master`分支,且**只需要最新的提交**, 则可以使用以下指令:

```sh
git clone -b master https://github.com/zhoukaisspu/testing.git --depth 1
```
