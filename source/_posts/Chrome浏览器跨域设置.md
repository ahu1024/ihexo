---
title: Chrome浏览器跨域设置
comments: false
tags:
  - Chrome
  - 浏览器跨域
date: 2018-03-28 09:52:36
updated: 2018-03-28 09:52:36
---

#版本号49之前的跨域设置
- Chrome 快捷图标在属性页面中的目标输入框里输入` "本机Chrome安装路径" --disable-web-security  `

#版本号49之后的跨域设置
- 在电脑上新建一个目录，例如：C:\MyChromeDevUserData
- Chrome 快捷图标在属性页面中的目标输入框里输入` "本机Chrome安装路径"  --disable-web-security --user-data-dir=C:\MyChromeDevUserData`