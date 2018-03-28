---
title: Hexo标签语法
tags:
  - hexo
  - markdown
date: 2018-03-27 19:56:12
updated: 2018-03-27 19:56:12
---

参考语法如下:

## 中间块

```
<center>中间块</center>
```

实例:
<center>中间块</center>

-----

## 固定大小图片

```
{% img /img/logo.png 200 200 Logo %}
```

实例:
{% img /img/logo.png 200 200 Logo %}

-----

## 代码引用块

```
  ```css  这是一段css https://www.baidu.com/ 原文链接
  #id{
    display: fles;
    color: red;
  }
  ```删
```

实例:
```css  这是一段css https://www.baidu.com/ 原文链接
#id{
  display: fles;
  color: red;
}
```