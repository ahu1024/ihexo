---
title: JS基础数据类型操作系列（一）字符串
tags:
  - JavaScript
  - String
date: 2018-04-20 01:20:57
updated: 2018-04-20 01:20:57
---

> String 对象用于处理文本（字符串）,一个字符串可以使用单引号或双引号.字符串的索引从零开始, 所以字符串第一字符为 [0],第二个字符为 [1], 等等。
或者你可以在字符串中使用转义字符 `\` ,
String 对象创建方法： (一) `var str = new String();`,（二）`var str = "string";`
String 对象属性包括 `constructor`对创建该对象的函数的引用;`length`字符串的长度;`prototype`允许您向对象添加属性和方法.
...................................................................................................

## 字符串方法

```js
("hello world")[1]                      // 输出 'e',获取特定位置的字符，兼容 IE8+
("hello world").charAt(1)               // 输出 'e',获取特定位置的字符
("hello world").charCodeAt(1)           // 输出 101,获取特定位置的字符编码
String.fromCharCode(104,101,108,108,111)// 输出 'hello' 静态方法将字符编码转换成字符串
```

## 字符串操作

```js
("hello").concat(' ','world')       // 输出 'hello world',字符串拼接，返回新的字符串（更常用的是 + 加号）
("hello world").slice(1,3)          // 输出 'el',参数分别是开始位置和结束为止，返回新字符串.参数为负值时将负值和长度相加
("hello world").subString(1,3)      // 输出 'el',参数分别是开始位置和结束为止，返回新字符串.参数为负值时全部转化为 0 
("hello world").substr(1,3)         // 输出 'ell'参数分别是开始位置和要截取的个数，返回新字符串.参数为负值时第一个参数要加长度，第二个转化为 0 
```

## 字符串位置方法

```js
("hello world").indexOf(" ")        // 输出 5，搜索给定的 子字符串位置（最后一个字符的位置），未找到返回 -1
("hello world").lastIndexOf(" ")    // 输出 5，从后向前搜索给定的 子字符串位置（最后一个字符的位置），未找到返回 -1
(" hello world ").trim()            // 输出 'hello world'， 删除前置和后缀的所有空格返回新字符串。
```

## 字符串大小写转换

```js
("hello world").toUpperCase()       // 输出 'HELLO WORLD', 转换成大写
("HELLO WORLD").toLowerCase()       // 输出 'hello world'，转换成小写
```

## 字符串模式匹配方法

```js
("hello world").match(/.o/)         // 输出 [ 'lo', index: 3, input: 'hello world' ]，参数是 正则表达式 或者 RegExp对象,失败返回 null
("hello world").search(/o/)         // 输出 4，参数是 正则表达式 或者 RegExp对象,成功返回第一个匹配项的位置，失败返回 -1
("hello world").replace('o','_')    // 输出 'hell_ world'，替换字符，第一参数是字符串，只替换第一个匹配项。（第二个参数可以是函数，请查资料）
("hello world").replace(/o/g,'_')   // 输出 'hell_ w_rld'，替换字符，第一参数是正则表达式且设置全局匹配，替换所有匹配项。
("hello world").split(' ')          // 输出 [ 'hello', 'world' ]，根据指定分隔符或者 RegExp 对象，将字符串分隔放入到数组中。
("a").localeCompare('c')            // 输出 -1，比较两个字符串字母在字母表中的位置用于排序，
("c").localeCompare('b')            // 输出 1 ，比较两个字符串字母在字母表中的位置用于排序，
("b").localeCompare('b')            // 输出 0 ，比较两个字符串字母在字母表中的位置用于排序，
```
