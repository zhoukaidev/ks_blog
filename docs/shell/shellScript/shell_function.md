# 简介

在编写`shell`脚本的过程中,经常会遇到需要重复使用某一块的代码，例如检查某个指令的返回值并根据返回值不同打印出相应的消息。

这时候需要通过`函数`来实现代码的重用。

## 定义函数

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

## 函数参数

在函数内部使用 `$1, $2,...$N` 来访问传入的不同的参数,其中`$1`代表第一个参数, `$N`代表第N个参数。

```sh
printParameters(){
    echo "First parameter: $1"
    echo "Second parameter: $2"
}

printParameters hello world

# 输出为
# First parameter: hello
# Second parameter: world
```

## 函数返回值

在`shell script`中，共有两种方式用于从一个函数中返回:

* 通过 `exit` 命令使得函数返回
* 通过 `return` 指令从函数内返回

在以上的两种返回方式中存在一些区别:

1. 当使用 `exit` 命令返回时，会终止整个脚本的执行,意味着该脚本后续的指令将不再执行
2. 当使用 `return` 命令返回时，只结束该函数的执行，函数后面的指令继续执行

**例程:**

```sh
ret_by_return() {
    echo "terminate function by return statement"
    return 0
}

ret_by_exit() {
    echo "terminate function by exit statement"
    exit 0
}

echo "invoke ret_by_return function"
ret_by_return
echo "end ret_by_return function"
echo "invoke ret_by_exit function"
ret_by_exit
echo "end ret_by_exit function"

# 输出值
# invoke ret_by_return function
# terminate function by return function
# end ret_by_return function
# invoke ret_by_exit function
# terminate function by exit statement
```

在以上的脚本中我们注意到 `echo "end return_by_exit function"` 命令并没有执行，应为 `ret_by_exit` 函数中调用 `exit` 指令进行函数返回。

  