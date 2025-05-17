# 简介

本文用于介绍 `env` 指令的相关用法。
`env`用于管理目前的环境变量，也可以用来动态修改环境变量后来运行相关的指令。
大部分情况下，我们会在脚本中用来指定相应的脚本解释器。

## 基本语法

```sh
env [OPTION]... [-][NAME=VALUE]... [COMMAND [ARG]...]
```

## 例程

* `env`，打印目前环境变量

```sh
# env 不带有任何参数
$ env
xxx
```

* `-i`或`--ignore-environment`:忽略所有环境变量

```sh
$ env -i
# 输出值为空
```

* 临时修改或添加环境变量

创建一个`user.py`脚本，用来打印`USER`环境变量：

```py
#!/usr/bin/env python3
import os
print(os.environ["USER"])
```

直接运行该脚本:

```sh
$ ./user.py
pi   #用户名为pi
```

修改`USER`环境变量值为`Hello`:

```sh
$ env USER="Hello" ./user.py
Hello #输出值变成Hello
```

## 总结

本人大部分是在脚本中使用`env`指令，通常是`shebang`指示符。
例如在写`python`脚本的时候，`shebang`经常看到两种写法:

* `#!/usr/bin/python3`
* `#!/usr/bin/env python3`

对于第一种写法是硬编码，强制要求Python3安装在`/usr/bin`目前下，但对于第二种写法则是
通过环境变量中的定义来寻找`python3`。

第二种写法可移植性更强，更为推荐。
