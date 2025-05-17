# 简介

本文主要用于记录一些在编写`shell script`的时候,常用的一些代码片段。

## 片段

### 获取脚本文件位置

```sh
#!/bin/bash

REL_PATH=$(dirname $0)
cd ${REL_PATH}
SCRIPT_PATH=$(pwd)
```
