# 用户界面

* 将图形界面切换为文字界面

```sh
$ sudo systemctl set-default multi-user.target
```

* 获取当前默认界面方式

```sh
$ sudo systemctl get-default
```

* 设置为图形界面

```sh
$ sudo systemctl set-default graphical.target
```
