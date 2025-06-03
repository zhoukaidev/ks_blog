# 简介

本文用于介绍在`shell script`与文件判断相关的操作符。

## 文件相关测试操作符

| 操作符     |   描述     |  例程     |
|-----------|------------|-----------|
| `-d file` | 检查该文件是否是文件夹，如果是，则返回`true` | `[ -d file ]` |
| `-f file` | 文件是否存在    | `[ -f file ]` |

### 例程

* `-d file`

```sh
CURRENT=`pwd`
FILE="${CURRENT}/test"
if [ -d "${FILE}" ]; then
    echo "It is directory"
else
    echo "It is not directory"
fi
```

