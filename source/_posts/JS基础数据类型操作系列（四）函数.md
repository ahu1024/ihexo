---
title: JS基础数据类型操作系列（四）函数
tags:

  - JavaScript
  - Function
date: 2018-04-20 13:10:05
updated: 2018-04-20 13:10:05
---

> 函数是对象，函数名是指向函数对象的指针，(重点：没有重载)所以当一个函数名被多次赋值不同的函数对象时，函数名只能指向和调用最后一次赋值的函数对象。下面主要介绍 `函数声明提升`、`闭包`、`arguments`、`arguments.callee`、`this`、`call`、`apply`、`bind`
> ...................................................................................................

## 函数声明提升

```js
console.log(fn);    // 成功执行，输出 ƒ fn(){console.log("ok")}。说明对函数声明进行了提升并解析
console.log(fn());  // 成功执行，输出 ok
function fn() {
  console.log("ok");
}
// 以上代码成功执行，是因为函数声明提升

console.log(fn);    // 执行成功，输出 undefined，
console.log(fn());  // 执行失败，报错 fn is not a function
var fn = function() {};
// 以上代码成功执行，是因为只进行了 变量声明提升，此时 fn 只是一个 undefined 的 变量名
```

## 闭包
函数作为`参数`或者`返回值`进行传递是闭包产生的必要条件
```js
// Callback 回调模式，也是 Promise 异步的原理
function a(callback){
    // do something
    callback();
}
function next(){
    // do something
}
a(next)
```

## 函数内部属性 arguments、callee、this

### arguments

类数组对象，保存函数参数

```js
factorial(5);
function factorial(num) {
  if (num <= 1) {
    return 1;
  } else {
    return num * factorial(num - 1);
  }
}

// 当函数没有函数名时，使用 arguments.callee
// callee是指针，指向拥有该`arguments`的函数本身，经典的阶乘函数：

(function(num) {
  if (num <= 1) {
    return 1;
  } else {
    return num * arguments.callee(num - 1);
  }
})(5);
```

### callee

ES 5 新对象属性，保存了调用当前函数的函数的引用（死循环执行？不可执行）

```js
a();
function a() {
  b();
}
function b() {
  console.log(b.caller);
} // 输出 ƒ a(){ b() } 严格模式不支持
```

### this

函数所在的执行环境对象（重点: this 是一个对象，可以是 window 或者某个自定义对象 Object）

```js
function fn() {
  var log = this === window;
  return log; 
}
fn();       // 输出 true
// 或者
var a = {
  some: function() {
    return this === window; 
  }
};
a.some();   // 输出 false
```

## prototype

原型，包含原型链上所有继承的属性和方法

## length

函数希望接受的命名参数的个数

## call || apply

函数默认拥有方法，在特定的作用域中调用函数，实际上是设置函数体内`this`对象的值。

```js
// fn.apply(this,[]) 第一个函数是其运行函数的作用域，第二个参数是 数组 或者 arguments 对象。
// fn.call(this,arg1,arg2...) 第一个函数是其运行函数的作用域，剩下的参数直接传递给函数。
function add(x, y) {
  console.log(x + y);
}
function counter1(x, y) {
  add.apply(this, arguments);   // apply 支持数组，类数组
}
counter1(1, 2); // 输出 3

function counter2(x, y) {
  add.call(this, x, y);         // call 支持多个参数
}
counter1(1, 2); // 输出 3

// 或者

window.color = "red";
var sky = { color: "bule" };
function whatColor() {
  console.log(this.color);
}
whatColor();            // 输出 red
whatColor.call(sky);    // 输出 bule
whatColor.apply(sky);   // 输出 bule
```

## bind

(ES 5)创建新实例，该实例的`this`值会绑定到传给`bind()`函数的值

```js
window.color = "red";
var sky = { color: "bule" };
function whatColor() {
  console.log(this.color);
}
whatColor();    // 输出 red
var newColor = whatColor.bind(sky);
newColor();     // 输出 bule
```
