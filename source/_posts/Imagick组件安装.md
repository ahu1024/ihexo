---
title: ImageMagick组件安装
tags:
  - ImageMagick
date: 2018-03-30 16:55:13
updated: 2018-03-30 16:55:13
---

> ImageMagick (TM) 是一个免费的创建、编辑、合成图片的软件。它可以读取、转换、写入多种格式的图片。图片切割、颜色替换、各种效果的应用，图片的旋转、组合，文本，直线，多边形，椭圆，曲线，附加到图片伸展旋转。ImageMagick的大多数功能的使用都来源于命令行工具。通常来说，它可以支持以下程序语言： Perl, C, C++, Python, PHP, Ruby, Java；现成的ImageMagick接口(PerlMagick, Magick++, PythonMagick, MagickWand for PHP, RubyMagick, and JMagick)是可利用的。这使得自动的动态的修改创建图片变为可能。
...................................................................................................

# 环境
```
- 系统 win 10
- php 5.6.25
- Apache 2.4.23
- wampServer 3.0.6 - 64bit 
```

# 第一步 查看 php.info 的以下信息
```
- Compiler	MSVC11 (Visual C++ 2012)
- Architecture	x64
- Server API	Apache 2.0 Handler
```
# 第二步 下载 php imagick 扩展
下载地址：[http://windows.php.net/downloads/pecl/releases/imagick/](http://windows.php.net/downloads/pecl/releases/imagick/)
根据第一步获取的信息，选择对应的版本： `2/2/2017  2:24 AM      7530033 php_imagick-3.4.3-5.6-ts-vc11-x64.zip`
其中 5.6 对应php版本，ts 对应 Server，vc11 对应 Compiler，x64 对应 Architecture；

# 第三步 配置扩展
 在 php.ini 配置文件中添加，`extension=php_imagick.dll`。
 将下载的扩展里的 `php_imagick.dll` 放到 php 文件的ext 目录下，例如: `C:\wamp64\bin\php\php5.6.25\ext\php_imagick.dll`
 将下载的扩展里的 全部 dll 文件（除了`php_imagick.dll`）放到 php 文件目录下，
 重启 wampServer ，即可在 php.info 页面看到 imagick 扩展加载成功，但是`ImageMagick supported formats` 为空，扩展还不可用，需要在系统安装 ImageMagick 软件。
 
# 系统安装 ImageMagick
 在 php.info 中获取一下信息：`Imagick using ImageMagick library version: ImageMagick 6.9.3-7 Q16 x64 2016-03-06 http://www.imagemagick.org`.
 所以我们需要安装的 ImageMagick 软件版本为 ImageMagick 6.9.3-7 Q16 x64；
 下载地址：[http://ftp.icm.edu.pl/packages/ImageMagick/binaries/](http://ftp.icm.edu.pl/packages/ImageMagick/binaries/)
 对应的软件全名：`ImageMagick-6.9.3-7-Q16-x64-dll.exe`
 
# 配置软件支持格式库
 在系统环境变量里添加ImageMagick安装后的图片格式支持库`coders`路径： `C:\Program Files\ImageMagick-6.9.3-Q16\modules\coders`
 
# 重启wampServer ，完成安装，开始测试
 
 在cmd 中测试
 ```
 打开windows 命令行窗口(win+r -> “cmd” -> Enter)，输入convert，回车。会出现convert的帮助文档，如果没有出现，说明没有安装成功，或没有把安装目录添加到环境变量 path 中。 
添加到环境变量，如我的 ImageMagick 安装目录是 c:/imagemagick。 
 ```
 在 PHP 中测试
 ```php
$im = new imagick( 'a.jpg' );
$im->thumbnailImage( 200, 0);
$im->writeImage( 'a_thumbnail.jpg' );
$im->clear();
$im->destroy();
header('Content-type: image/jpeg');
echo $im;
 ```
 
 
 
 