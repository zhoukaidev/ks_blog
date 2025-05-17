# 简介

本文用于记录`tmux`的相关用法。

## 指令集合

本文主要介绍以下分类:

* attach session
* detach session
* create pane
* manage session
    * create session
    * kill session
* resize pane

### attach session

与`attach session`有关的指令如下:

| 指令   |   介绍  |
|-------|---------|
| `tmux ls` |  显示目前所有的`session` |
| `tmux attach -t [sessionNumber]`  | 根据*session number*链接session|

### detach session

| 指令    |  介绍  |
|---------|--------|
| `tmux detach` |  与当前的`session`断开连接 |
| `"Ctrl+b"` -> d  | 使用快捷键断开`session`连接，先按`Ctrl+b`,松开后按`d`  |

### manage session

| 指令     | 介绍   |
|----------|--------|
| `tmux kill-server`  | kill server,删除所有的`session` |
|在默认终端中输入`tmux`  | 创建一个新的session |
| `tmux rename-session -t 0 mysession` |  将session 0重命名为`mysession` |
| `tmux new-session -s mysession` | 创建新的`session`,并命名为`mysession` |
| `tmux new -s mysession` | 同 `tmux new-session -s mysession` |

### create pane

在一个`session`中，我们可以创建多个`pane`来同时进行工作

| 指令      |  介绍    |
|----------|-----------|
| `"Ctrl+b"` -> %  | 垂直切分window |
| `"Ctrl+b"` -> "  | 水平切分window  |
| `"Ctrl+b"` -> arrow | 在多个`pane`中切换焦点 |

### resize pane

1. 按住`Ctrl+b`的同时，快速按`左键`或`右键`调节宽度

> 这里必须是按住`Ctrl+b`的同时按`左键`或`右键`

### view history

在tmux的默认环境中,"鼠标滚轮"的事件会被映射称为"上下"按键的功能,因此我们无法直接使用"鼠标滚轮"去查看历史。
我们可以通过一些快捷键进入`copy mode`,然后通过"上下"按键去查看历史。

| 指令     |  介绍      |
|---------|------------|
| `"Ctrl"+b` ->'\['| Enter copy mode to copy text or view the history |
| `q`    |  进入`copy mode`后使用`q`来退出`copy mode`   |

进入`copy mode`之后就可以使用`鼠标滚轮`或者`上下`按键来查看console的历史输出了。

## FAQ

> 在进入`tmux`后,无法显示正常`bash`设置的语法高亮?

* 将以下代码添加到`~/.tmux.conf`文件中:
```sh
set -g default-terminal "screen-256color"
```

## 参考文档

* [Easy guide to tmux](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
* [How do i scroll in tmux](https://superuser.com/questions/209437/how-do-i-scroll-in-tmux)
