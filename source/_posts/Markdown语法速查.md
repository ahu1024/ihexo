---
title: Markdown语法速查
comments: false
tags:
  - Markdown
date: 2018-03-28 09:15:03
updated: 2018-03-28 09:15:03
---


> Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。
Markdown具有一系列衍生版本，用于扩展Markdown的功能（如表格、脚注、内嵌HTML等等），这些功能原初的Markdown尚不具备，它们能让Markdown转换成更多的格式，例如LaTeX，Docbook。
...................................................................................................
# 标题 Title
## 类 Setext 形式标题

```
This is an H1
=============

This is an H2
-------------
```

## 类 atx 形式标题

```
# 这是 H1
## 这是 H2
...
###### 这是 H6
```

# 区块引用 `Blockquotes`
## 自定义断行区块引用

```
> Markdown 标记区块引用是使用类似 email 中用 > 的引用方式。
> 如果你还熟悉在 email 信件中的引言部分，
> 你就知道怎么在 Markdown 文件中建立一个区块引用，
> 那会看起来像是你自己先断好行，然后在每行的最前面加上 > 
```

## 自动断行区块引用

```
> Markdown 标记区块引用是使用类似 email 中用 > 的引用方式。如果你还熟悉在 email 信件中的引言部分，你就知道怎么在 Markdown 文件中建立一个区块引用，那会看起来像是你自己先断好行，然后在每行的最前面加上 > ,Markdown 也允许你偷懒只在整个段落的第一行最前面加上 > .
```

## 多层嵌套区块引用

```
> ## 这是一个标题。
> 
> >1.   这是第一行列表项。
> >2.   这是第二行列表项。
> 
```

# 列表 List
## 有序列表

```
1. 第一行
1. 第一行
1. 第一行
```

## 无序列表

```
* 第一行
- 第二行
+ 第三行
+ 如果要在列表项目内放进引用，那 > 就需要缩进：
	> This is a blockquote
    > inside a list item.
+ 如果要放代码区块的话，该区块就需要缩进两次，也就是 8 个空格或是 2 个制表符：
		<code>
+ 如果行首出现`数字-句点-空白`，要避免误产生列表项，你可以在句点前面加上反斜杠。
1986\. What a great season.
```

# 代码区块 CodeBlock
## 标签形式

```
删```删
上下都是三个`符(去除反斜杠)
删```删
```

## 缩进形式

```
&nbsp;&nbsp;&nbsp;&nbsp;前面是4个空格
——>前面是一个TAB制表符
```

## 行内代码区块

```
  `   文本前后用 "`" 包围   `
  
  代码区段内插入反引号，你可以用多个反引号来开启和结束代码区段：
  ``开启   括号内 (`) 不编译   结束``
  
  代码区段的起始和结束端都可以放入一个空白，起始端后面一个，结束端前面一个，这样你就可以在区段的一开始就插入反引号：
  A single backtick in a code span: `` ` ``
  A backtick-delimited string in a code span: `` `foo` ``
```

# 分隔线  Separation line

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

```
* * *
***
*****
- - -
---------------------------------------
```

# 链接 Link
## 绝对路径

```
[瞄文本](http://example.com/ "Title：可省略")
[瞄文本](http://example.com/ )
```

## 相对路径

```
[瞄文本·本地域名下](/about/) 
```

## 参考式的链接

```
在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：
This is [an example][id] reference-style link.

你也可以选择性地在两个方括号中间加上一个空格：
This is [an example] [id] reference-style link.

接着，在文件的任意处，你可以把这个标记的链接内容定义出来：
[id]: <http://example.com>  "Optional Title Here"
[id]: http://example.com "Optional Title Here"
[id]: http://example.com (Optional Title Here)
[id]: <http://example.com>
    (Optional Title Here)
```

## 隐式链接标记功能

```
链接标记会视为等同于链接文字
[Google][]

链接标记也可以定义链接内容（可省略）
[Google]: http://google.com/
```

## 自动连接

```
<http://example.com/>   编译后   <a href="http://example.com/">http://example.com/</a>
<address@example.com>   编译后   <a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>
```

# 强调
Markdown 使用星号（`*`）和底线（`_`）作为标记强调字词的符号，被 `*` 或 `_ `包围的字词会被转成用` <em> `标签包围，用两个 `* `或` _ `包起来的话，则会被转成 `<strong>`，例如：

```
*single asterisks*       //斜体

_single underscores_      //斜体

**double asterisks**		//粗体

__double underscores__		//粗体

如果你的 * 和 _ 两边都有空白的话，它们就只会被当成普通的符号。
```

# 图片 Picture

## 行内式

```
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
```

## 参考式

```
![Alt text][id]

「id」是图片参考的名称，图片参考的定义方式则和连结参考一样：
[id]: url/to/image  "Optional title attribute"
```

# 转义反斜杠字符 `/`

Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号，例如：如果你想要用星号加在文字旁边的方式来做出强调效果（但不用 `<em>` 标签），你可以在星号的前面加上反斜杠：

```
\*literal asterisks\*

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```

# 表格

```
|左对齐| 居中 | 右对齐|
| ---- |:----:| ----:|
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |
```
|左对齐| 居中 | 右对齐|
| ---- |:----:| ----:|
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |
| 内容 | 内容 | 内容 |

# 参考资料

[Markdown——入门指南](http://www.jianshu.com/p/1e402922ee32# "Title：Markdown——入门指南")
[我基百科](http://zh.wikipedia.org/wiki/Markdown "Title：Markdown")
[Markdown 快速入门](https://segmentfault.com/a/1190000000724183#articleHeader10 "Title：Markdown 快速入门")

