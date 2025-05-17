# 简介

本文主要介绍`wget`的基本用法。 Record these to save my bad memory. :)

## 基本用法

|   形参(短类型)  |   形参(长类型)   |  描述     |    示例    |
|----------------|-----------------|-----------|------------|
| -          |    -               | 直接保存`index.html`到本地  | `wget https://www.example.com/index.html` |
| `-q`      | `--quite`     | Turn off Wget's output   | `wget -q https://www.example.com/index.html`  |
| `-O file`      | `--output-document=file` | The documents will be concatenated together and written to file | `wget -q -O - https://example.com/index.html` 将index.html通过console输出 |
