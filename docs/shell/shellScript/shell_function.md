# 简介

在编写`shell`脚本的过程中,经常会遇到需要重复使用某一块的代码，例如检查某个指令的返回值并根据返回值不同打印出相应的消息。

这时候需要通过`函数`来实现代码的重用。


# 定义函数

```sh
function_name() {
    # function body
}
```

* `function_name` 用于定义函数的名称
* 在 `{}` 内书写需要执行的代码

**例程**:

```sh
# 定义printLog函数用于打印log,在log前添加该log被打印的时间
printLog() {
    DATATIME=`data`
    echo "{DATATIME}: $1"
}
```

# 函数参数

在函数内部使用 `$1, $2,...$N` 来访问传入的不同的参数,其中`$1`代表第一个参数, `$N`代表第N个参数。

```sh
function printParameters(){
    echo "First parameter: $1"
    echo "Second parameter: $2"
}

printParameters hello world

# 输出为
# First parameter: hello
# Second parameter: world
```

# 函数返回值

