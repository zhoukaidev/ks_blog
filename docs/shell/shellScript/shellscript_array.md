# 简介

本文用于介绍如何在`shell script`使用`数组`。

## 定义数组

```sh
#!/bin/sh
#该语法用于定义数组，其中数组包含variable1, variable2, variable3
ARRAY=(variable1 variable2 variable2)
```

## 数组操作

```sh
#!/bin/sh
ARRAY=(varialbe1 variable2 variable3)
# 数组中的所有元素
echo ${ARRAY[*]}
echo ${ARRAY[@]}
#数组中的所有下标
echo ${!ARRAY[*]}
# 数组的长度
echo ${#ARRAY[*]}
# ARRAY[0]的长度
echo ${#ARRAY[0]}
```

## 数组长度

```sh
#!/bin/sh

ARRAY=(variable1 variable2 variable3)
len=${#ARRAY[*]}
```
## 访问数组元素

```sh
#!/bin/sh
#使用下标的方式访问数组元素
ARRAY=(variable1 variable2 variable3)
# 返回所有元素
echo ${ARRAY[*]}
echo ${ARRAY[@]}
#根据下标返回元素
echo ${ARRAY[0]}
echo ${ARRAY[1]}
echo ${ARRAY[2]}
```
## for遍历

```sh
#!/bin/sh
ARRAY=(variable1 variable2 variable3)
for x in "${ARRAY[@]}"
do
    echo $x
done
```
