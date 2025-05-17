## 简介

本文会从该网站的生成到部署做一个详细的介绍,并将中途遇到的问题做一个总结。
后续会分为两个部分进行介绍:

* 借助[MkDocs](https://www.mkdocs.org/)生成网站
* 借助[Travis CI](https://travis-ci.com/)来实现网站的自动部署
  
因为网站的生成与部署都可以实现自动化,所以我们可以更加专注于文档的内容。

在整个流程中，首先将使用`markdown`编写的文档`push`到远程仓库中，一次新的commit
会触发`Travis CI`来开始工作，tarvis-ci会首先编译最新的工程文档，生成静态站点,
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

## 网站自动部署

网站的自动部署过程是借助[Travis-CI](https://travis-ci.org/)来完成的。

Travis-CI内置了对于[部署到github page](https://docs.travis-ci.com/user/deployment/pages/)的支持。但是需要提供[personal access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line),这会将所有仓库的读写权限全部
开放出去,个人不太喜欢这种做法。后面介绍使用[Deploy key](https://developer.github.com/v3/guides/managing-deploy-keys/)来完成自动部署的功能。

### 使用personal acess token部署网站

请参考[如何使用personal access token部署网站](https://docs.travis-ci.com/user/deployment/pages/).

### 使用Deploy key部署网站

在进行后续步骤之前，将当前的工作目录切换到已经在`Travis-CI`配置好的仓库目录下面。


* 生成`Deploy key`

```bash
$ ssh-keygen.exe -t rsa -b 4096 -C "Your email" -f deploy-key
# 在Enter passphrase的时候，不要输入任何密码
# 公私密钥创建完成后，在当前目录中可以看到生成的密钥文件
# 其中deploy-key.pub为公钥文件， deploy-key为私钥文件
```
* [将公钥添加到相应的仓库中](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys)

在将公钥添加到相应仓库的时候,要确保`Allow write access`勾选上，因为后续
要通过`Travis-CI`将网站`push`到该仓库中。

* [安装`Travis-CI`客户端](https://docs.travis-ci.com/user/encrypting-files/#prerequisites)

```bash
$ gem install travis
```
* 登录Travis-CI并加密私钥文件
   
首先切换到已经在`Travis-CI`设置的仓库目录下面。

```bash
$ travis login --com
$ 一些登录信息
# 该步骤会加密私钥文件，并将相应的解密脚本添加到.tarvis.yml文件中
$ travis encrypt-file deploy-key --add
xxx(一些log信息)
```

* 配置.travis.yml文件
   
配置文件的详细内容请参考[配置.travis.yml实现github page的自动部署](https://github.com/zhoukaisspu/ks_blog/blob/master/.travis.yml).

* 提交相应的文件
   
将`.tarvis.yml`及`deploy-key.enc`文件提交到远程仓库中。

!!! warning
    在文档提交过程中，切记一定**不要**将`deploy-key`及`deploy-key.pub`
    提交到远程仓库中，将`deploy-key`提交到仓库中会直接泄露你的私钥。

## F.A.Q

!!! question
    在使用`Travis-CI`中出现如下错误:
    139785287845536:error:0606506D:digital envelope routines:EVP_DecryptFinal_ex:wrong final block length:evp_enc.c:532:
    The command "openssl aes-256-cbc -K $encrypted_5a7cb78de077_key -iv $encrypted_5a7cb78de077_iv -in deploy-key.enc -out deploy-key -d" failed and exited with 1 during .

> 解决办法: 我是在windows系统中生成的`deploy-key.enc`,此时的换行标识符为`\r\n`,在linux系统下换行符为`\n`,
> 所以可以使用`dos2unix`工具将该文件转换成为linux格式即可。
