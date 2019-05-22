## 简介

本文会从该网站的生成到部署做一个详细的介绍,并将中途遇到的问题做一个总结。
后续会分为两个部分进行介绍:

* 借助MkDocs生成网站
* 借助travis-ci来实现网站的自动部署
  
因为网站的生成与部署都可以实现自动化,所以我们可以更加专注于文档的内容。

在整个流程中，首先将使用`markdown`编写的文档`push`到远程仓库中，一次新的commit
会触发`travis-ci`来开始工作，tarvis-ci会首先编译最新的工程文档，生成静态站点,
紧接着将该站点push到`github.io`上,当然所有的工作都是自动化完成的。

## 使用MkDocs生成网站

MkDocs是将使用Markdown编写的工程文档编译成静态站点的一个工具,详细的信息可以参考
官方网站。

* 安装相应的工具
  1. [安装MkDocs](https://www.mkdocs.org/#installation)
  2. [安装Material for MkDocs(该网站主题)](https://github.com/squidfunk/mkdocs-material)

```bash
# 验证mkdocs是否安装成功
$ mkdocs --version
mkdocs, version 1.0 from YOUR/INSTALL/PATH
```

* [生成工程目录](https://www.mkdocs.org/#getting-started)
* [修改配置文件](https://www.mkdocs.org/user-guide/configuration/) 
  1. 修改站点名称`site_name`(可选)
  2. [创建文档布局](https://www.mkdocs.org/user-guide/configuration/#documentation-layout)

* [设置网站主题](https://www.mkdocs.org/user-guide/styling-your-docs/)

!!! note 
    在实际的配置过程中,可以使用`mkdocs serve`来命令来预览生成的站点样式。
    详细内容请参考[mkdocs serve命令](https://www.mkdocs.org/#getting-started).

