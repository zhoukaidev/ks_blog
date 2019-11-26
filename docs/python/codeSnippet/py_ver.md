# 简介

本文主要用于简介如何获取`python`的版本号。

在日常开发中，我们经常需要判断目前的运行环境是否符合要求，并在不符合要求的情况下执行一些特殊的指令。

## 获取版本

```py
import sys
ver_info = sys.version_info
major = ver_info.major
minor = ver_info.minor
micro = ver_info.micro
print("sys.version_info:", sys.version_info)
print("major:", major)
print("minor:", minor)
print("micor:", micro)
```

## 版本校验

```py
# 校验版本 >=3.7.2
# 如果不符合，则返回1
import sys
major = sys.version_info.major
minor = sys.version_info.minor
micro = sys.version_info.micro
if ((major < 3) or (major ==3 and minor < 7) or (major ==3 and minor == 7 and micro < 2)):
    sys.exit(1)
```
我们就可以在`shell`脚本中来调用这个`python`脚本,通过判断`python`脚本的返回值来判断版本是否符合我们的要求。
