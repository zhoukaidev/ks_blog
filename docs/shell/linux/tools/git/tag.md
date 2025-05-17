# 简介

本文主要用于介绍`git tag`的使用。

在日常的代码管理中,当我们的代码开发到达某个阶段的时候,我们会经常选择在某个节点添加`tag`,用于标识该节点代码的作用。
例如我们可能会在某个节点添加`v1.0`的节点,用于标识该节点的代码为发布版`1.0`.

## Tag 类型

git支持两种不同类型的`tag`：

* lightweight(轻量级)
* annotated(带注释)

### 添加lightweight的tag

```sh
# 添加v1.0标签到最新的节点
git tag v1.0
```

### 添加annotated的tag

```sh
# 添加v1.0标签到最新的节点,并添加相应的tag信息
git tag -a v1.0 -m "This is my v1.0 release"
```


### 将tag推送的远程服务器

默认情况下, git并不会将本地的tag推送到远端服务器, 如果确实需要将这些tag推送到远端服务器,可以采用如下指令:

```sh
# 推送所有的tag到远端服务器
git push origin --tags

# 推送单个tag到远端服务器
# 将v1.0的tag推送至远端服务器
git push origin v1.0
```
