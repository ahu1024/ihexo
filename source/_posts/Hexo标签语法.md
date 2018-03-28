---
title: Hexo标签语法
tags:
  - Hexo
  - Markdown
date: 2018-03-27 19:56:12
updated: 2018-03-27 19:56:12
---

> 标签插件和 Front-matter 中的标签不同，它们是用于在文章中快速插入特定内容的插件。但是在markdown 中添加太多的hexo 标签，其实会在以后用其他编辑器预览，查看，迁移时留下诸多不变，毕竟，私有的语法意味着不兼容，本文只选取了常用的三个作为示例。
...................................................................................................

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