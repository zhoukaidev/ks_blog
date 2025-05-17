# 简介

本文主要介绍`curl`指令在`Linux or Windows`下的使用方法。

## 下载文件

| 形参(短类型)    | 形参(长类型)  |  描述     |   例程   |
|----------------|--------------|-----------|----------|
| `-o [fileName]` | `--output`  |下载指定的文件，并写入到fileName中 | `curl -o output.html http://example.com/` |
| `-O`(uppercase letter o) | -- |下载指定文件, 本地文件名称和远端文件名相同  | `crul -O http://www.netspace.com/index.html` |
| `-v`       | `--verbose` | 使curl打印出详细的信息，可用于调试等功能  | `curl -v http://www.example.com/` |
| `-i`   | `--include`   | 在output中包含http response header   |  `curl -i https://www.baidu.com`  |
| `-I`  | `--head`  | 仅提取document header  | `curl -I https://www.example.com` |

## 安全认证

| 形参(短类型)  | 形参(长类型)   | 描述    | 例程   |
|-------------|----------------|---------|-------|
| `-u <user:passworld>` |  `--user <user:passworld>` | 指定用户名及密码   |  `curl --user Username:Password  http://example.com` |
