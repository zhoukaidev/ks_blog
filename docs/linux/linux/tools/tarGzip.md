# 简介

该文主要介绍`linux`下的`打包`及`压缩`指令。

## gzip

* `gzip [-cdtv#] 文件名`

| 参数    |  简介     |
|---------|-----------|
|`-c --stdout --to-stdout` | 将压缩数据输出到屏幕，可以重定向该数据 |
|`-d --decompress --uncompress` | 解压数据  |
| `-v --verbose` | 显示压缩率和名称信息  |
| `-k --keep` | 保留压缩或解压的输入文件  |

## tar

* `tar [-z | -j | -J] [cv] [-f 新文件名] 待打包文件` #打包与压缩
* `tar [-z | -j | -J] [tv] [-f 新文件名] tar文件名` #查看内部文件名
* `tar [-z | -j | -J] [xv] [-f 新文件名] tar文件名 [-C 目录]` #解压缩及解包

| 参数     | 简介     |
|----------|----------|
| `-c --create` | 创建新的打包文件   |
| `-x --extract --get` | 从打包文件中抽取文件 |
| `-f --file` | 指定archive的名称    |
| `-z`  | gzip进行压缩或解压缩, .tar.gz   |
| `-j`  | bzip2压缩或解压缩, .tar.bz2  |
| `-J` | xz进行压缩或解压缩, .tar.xz  |
| `-C --directory=DIR`  | 切换到DIR目录下进行解压缩动作  | 
| `-t --list` | 列出打包文件里的内容 |

