## 简介

本文主要记录与`xcode`工程相关的自动化编译过程,为了实现自动化编译的动作，我们使用了`xcodebuild`工具，
后续内容主要分为以下几个方面:

* 编译(Build)
    * 指定方案(scheme)
    * 指定工作空间(workspace)  
    * 修改编译版本(Debug/Release)
    * 修改编译设置(buildSetting)
    * 指定输出路径(derived data path)
* 打包(Archive)
    * 生成archive文件(file.xcarchive)
    * 基于archive文件导出其他文件(distributed)
* 代码签名(Code sign)
    * 什么是代码签名
    * 代码签名的基本流程
    * 配置`xcode`实现代码签名
* 参考文档

## 编译(Build)

在日常使用`xcode`进行代码开始时,可以选择使用工具栏中提供的`Build`,`Run`等按钮来执行代码编译，运行等工作，
但对于CI/CD而言，我们需要使用命令行工具来完成这些动作，这里我们使用`xcodebuild`工具。

编译过程用到了`xcodebuild`提供的`"build"` action。

* 指定方案(scheme)

    通过使用 `"-scheme xxx"` 配置scheme。

* 指定工作空间(workspace)

    通过使用 `"-workspace xxx"` 配置workspace。

* 修改编译版本(Debug/Release)

    通过使用 `"-configuration xxx"` 配置`Debug/Release`等。

* 指定编译设置(buildSetting)

    通过 `"buildsetting=value"` 来将某个编译配置设置为某个值。详细内容可以通过 `"man xcodebuild"`查看。

* 指定输出路径(derived data path)

    通过 `"-derivedDataPath xxx"` 设置输出路径
    
```sh
# scheme为myScheme
# workspace为myWorkSpace.xcworkspace
# configuration为Release
# 将编译设置中的DEVELOPMENT_TEAM设置为XXX
$ xcodebuild -scheme myScheme\
    -workspace myWorkSpace.xcworkspace/\
    -configuration Release\
    DEVELOPMENT_TEAM=XXX\
    -derivedDataPath $PWD/build
```


## 打包(Archive)

`xcodebuild` 使用 `archive` 动作来实现打包。

* 生成archive文件

    - `"-archivePath xxx"` 指定生成的archive路径
    - `"-scheme xxx"` 指定scheme
    - `"-workspace xxx"` 指定workspace

    
    > 当指定 `archive` 动作的时候，`"-archivePath xxx"` 用于指定生成的archive路径。
    > 
    > 当传入了`"-exportArchive xxx"` 或 `"-exportNotarizedApp"` 参数时, `"-archivePath xxx"` 则用于指定需要
    > 导出的archive路径。

```sh
# archive指定archive action
# scheme为myScheme
# workspace为myWorkSpace.xcworkspace/
$ xcodebuild archive -scheme myScheme -workspace myWorkSpace.xcworkspace/
```

* 根据archive文件导出其他文件(distributed)
    - `"-exportArchive "` 指定archive文件应该被分发(distributed)。
    - `"-archivePath xxx"` 指定待分发的archive文件路径
    - `"-exportPath xxx"` 指定导出文件的存储路径
    - `"-exportOptionsPlist xxx.plist"` 配置导出何种类型文件

```sh
# archive文件为myArchive.xcarchive
# 导出文件存储路径exportedFilePath
# 配置文件为 myOption.plist
$ xcodebuild -exportArchive -archivePath myArchive.xcarchive\
     -exportPath exportedFilePath\
     -exportOptionsPlist myOption.plist
```

## 代码签名(code sign)

### 什么是代码签名

代码签名是指通过数学运算对可执行程序和脚本等文件进行**数字签名**，我们使用该`数字签名`来校验
该软件的确是软件发布者所发布的软件，在传播过程中没有被中间人进行过修改。

### 代码签名的基本流程

在介绍后续的代码签名流程之前，我们需要先理解非对称加密的概念。

* 非对称加密
    - 公钥
    - 私钥

    非对称加密中存在`公钥-私钥`的概念：

    * 数据通过私钥加密后，只能通过公钥才能解密
    * 数据通过公钥加密后，只能通过私钥才能解密

当然这里所说的`只能通过xxx才能解密`是指通过其他方式进行解密会花费及其大的资源。

```
 original data             encrypted data
+-------------+  encrypted  +--------------+ decrypted   +------------+
| hello       | private key | xx.jfslflwef | public key  | hello      |
|             |-----------> | 90*fsem;wskf |-----------> |            |
+-------------+             +--------------+             +------------+
```

* 签名基本流程
    1. 开发者持有相关机构颁发的证书
    2. 对相关程序及脚本计算哈希值
    3. 开发者使用自己的私钥对哈希值进行加密计算,生成数字摘要
    4. 将数字摘要，证书及相关可执行程序打包进行发布


* 验证代码签名
    1. 验证程序通过使用颁发机构的证书来验证开发者证书的有效性(后续假设开发者证书有效)
    2. 验证程序对开发者发布的程序生成哈希值
    3. 验证程序对开发者发布程序中包含的数字摘要进行解密，得到原始哈希值
    4. 如果验证程序生成的哈希值与解密得到的哈希值相同，代表发布的程序未被篡改

## 参考文档

* [Code Signing Guide](https://developer.apple.com/library/archive/documentation/Security/Conceptual/CodeSigningGuide/Procedures/Procedures.html)
* [Understanding Digital Certificates and Code signing](https://www.oracle.com/technetwork/java/javase/documentation/digitalcerts-codesigning-4312830.html)
* [CACS-Cdoe-Signing](https://casecurity.org/wp-content/uploads/2016/12/CASC-Code-Signing.pdf)
* [xcodebuild](https://developer.apple.com/library/archive/technotes/tn2339/_index.html#//apple_ref/doc/uid/DTS40014588-CH1-HOW_DO_I_ARCHIVE_AND_EXPORT_MY_APP_FOR_DISTRIBUTION_)
* [How to check the universal macOS binary](https://developer.apple.com/documentation/apple-silicon/building-a-universal-macos-binary)
