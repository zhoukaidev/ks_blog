# 简介

本文主要用于介绍`OCR`相关的内容总结。

* OCR开源库
    * [Tesseract](https://github.com/tesseract-ocr/tesseract)

## Tesseract

* 参考文档
    * [Tesseract Page Segmentation Modes: how to imporve your OCR accuracy](https://pyimagesearch.com/2021/11/15/tesseract-page-segmentation-modes-psms-explained-how-to-improve-your-ocr-accuracy/)


### 页面分割模型

Tesseract的页面分割模型对于OCR识别的准确率有着很大的影响,在实际使用Tesseract的时候,需要学会如何选择正确的页面分割模型(PSMs)。

默认情况下， Tesseract期望得到一页文本(page of text)作为输入数据,这意味着当输入一页数据的时候,默认的PSM可以工作的很好,但是当输入一行文本,一个单词或者单个字符的时候,OCR的结果可能就很不理想。


`tesseract --help-psm`可以显示目前所有的psm:

```
Page segmentation modes:
  0    Orientation and script detection (OSD) only.
  1    Automatic page segmentation with OSD.
  2    Automatic page segmentation, but no OSD, or OCR. (not implemented)
  3    Fully automatic page segmentation, but no OSD. (Default)
  4    Assume a single column of text of variable sizes.
  5    Assume a single uniform block of vertically aligned text.
  6    Assume a single uniform block of text.
  7    Treat the image as a single text line.
  8    Treat the image as a single word.
  9    Treat the image as a single word in a circle.
 10    Treat the image as a single character.
 11    Sparse text. Find as much text as possible in no particular order.
 12    Sparse text with OSD.
 13    Raw line. Treat the image as a single text line,
       bypassing hacks that are Tesseract-specific.
```

### 编译

* 安装`visual studio`,并通过`visual studio installer`安装cmake工具
* 下载[software network client工具](https://software-network.org/client/sw-master-windows-client.zip)
* 将上一步下载`sw.exe`添加到环境变量,这样可以在`cmd`中直接调用`sw.exe`命令
* 运行`sw setup`命令(可能需要管理员权限)
* 使用`git`克隆tesseract源码
* `cd tesseract`
* `mkdir build && cd build`
* 使用管理员权限打开`developer command prompt for vs2022`,然后在`build`文件夹中运行`cmake ..`
* 运行完上述命令后, 会生成`tesseract.sln`,同时会调用`sw`工具下载所需要的依赖项
* 编译上述的工具，可以得到`libtesseract`和`tesseract.exe`
* 如果编译`release`版本失败，需要修改一下链接的库

```md
the debug libraries are
  concrtd.lib
  msvcprtd.lib
  vcruntimed.lib
  msvcrtd.lib
  ucrtd.lib
Change them to release by removing the letter "d"
  concrt.lib
  msvcprt.lib
  vcruntime.lib
  msvcrt.lib
  ucrt.lib
```

### 运行

* `tesseract.exe --help`
    * 查看帮助文档
* `tesseract.exe --help-extra`
    * 针对高级用户，提供的其他更加丰富的配置选项
* `tesseract.exe imagename output --oem 1 -l eng --psm 1`
    * 识别指定的文件，并按照指定格式进行输出