---
title: Chrome浏览器跨域设置
tags:
  - Chrome
  - 浏览器跨域
date: 2018-03-28 09:52:36
updated: 2018-03-28 09:52:36
---

> 做前后分离的webapp开发的时候，出于一些原因往往需要将浏览器设置成支持跨域的模式，好在chrome浏览器就是支持可跨域的设置，网上也有很多chrome跨域设置教程。但是新版本的chrome浏览器提高了跨域设置的门槛，原来的方法不再适用了。下面笔者简单介绍一下新版本chrome的跨域设置方法
...................................................................................................

#版本号49之前的跨域设置
- Chrome 快捷图标在属性页面中的目标输入框里输入` "本机Chrome安装路径" --disable-web-security  `

#版本号49之后的跨域设置
- 在电脑上新建一个目录，例如：C:\MyChromeDevUserData
- Chrome 快捷图标在属性页面中的目标输入框里输入` "本机Chrome安装路径"  --disable-web-security --user-data-dir=C:\MyChromeDevUserData`