---
title: JS基础数据类型操作系列（补充）
tags:
  - JavaScript
date: 2018-04-20 15:46:56
updated: 2018-04-20 15:46:56
---

> Global (全局)对象是一个虚拟概念，也就是说不属于其他对象的操作方法和属性，最终都是全局对象的。但是在web浏览器中都将这个全局对象作为Window对象的一部分来加以实现和调用。
...................................................................................................

一些常见的属性概念和属相检测方法

```js
false                                       // 0,'',null,undefined,false,NaN
null                                        // 空对象指针
undefined                                   // 未初始化的变量，由null派生而来
eval('console.log("evel")')                 // 完整强大的 ECMAScript 解析器
instanceof                                  // object instanceof constructor 检测 constructor.prototype 是否存在于参数 object 的原型链
typeof []                                   // 输出 object，检测变量的数据类型
isNaN()                                     // 非数值型数据检测，自身不相等(null != null)
isFinite()                                  // 检测某个数值是否在最大值（Number.MAX_VALUE）和最小（Number.MIN_VALUE）之间
parseInt()                                  // 强制转换为整数，第二个参数可以指定进制格式(最好每次都带上进制，例如 parseInt("010",10))
parseFloat()                                // 强制转换为小数类型。
encodeURI('http://baidu.com')               // 输出 'http://baidu.com'，适用于编码 domain
decodeURI('http://baidu.com')               // 输出 'http://baidu.com'，适用于解码 domain
encodeURIComponent('/api?name=baidu')       // 输出 '%2Fapi%3Fname%3Dbaidu' ，适用于编码 API参数
decodeURIComponent('%2Fapi%3Fname%3Dbaidu') // 输出 '/api?name=baidu',适用于解码 API参数
Array.isArray([]);                          // 返回 true
Number.toString(/*n进制,默认为10进制*/)      // 例如 10.toString(2) 输出 '1010'
Number.toFixed(/*指定小数位*/)               // 适合处理货币，四舍五入.例如(10.004).toFixed(2) 输出 10.00
Object.hasOwnProperty("key")                // 检查属性是不是对象自己的，忽略掉那些从原型链上继承到的属性。
Object.prototype.toString.call([])          // 输出 [object Array]，检测引用类型的原型
```