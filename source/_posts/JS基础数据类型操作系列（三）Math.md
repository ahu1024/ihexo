---
title: JS基础数据类型操作系列（三）Math
tags:
  - JavaScript
  - Math
date: 2018-04-20 11:57:09
updated: 2018-04-20 11:57:09
---

> Math 对象包含了数学公式和信息。比如常用的值有`自然对数的底数 Math.E`,`圆周率 Math.PI`，`2的平方根 Math.SORT2`等，常用数学公式方法有`最小值 Math.min()`,`最大值 Math.max()`,`向上舍入Math.ceil()`,`向下舍入 Math.floor()`,`四舍五入 Math.round()`,`0到1随机数 Math.random()`,`绝对值 Math.abs`
> ...................................................................................................

## min() 和 max()

用于确定一组数值中的最小值和最大值。

```js
// 常规
Math.min(1, 22, 35, 67, 63, 3); // 输出 1
Math.max(1, 22, 35, 67, 63, 3); // 输出 67
Math.min.apply(Math, [1, 22, 35, 67, 63, 3]); // 输出 1
Math.max.apply(Math, [1, 22, 35, 67, 63, 3]); // 输出 67
// 特例
Math.max("1", 22, 35, "67", 63, 3); // 输出 67
Math.max("1", 22, 35, "67", 63, 3, "a"); // 输出 NaN
Math.min("1", 22, 35, "67", 63, 3, ""); // 输出 0
```

## 舍入方法
舍入规则包括 向上取整，向下取整，四舍五入
```js
Math.ceil(10.55)        // 输出 11
Math.ceil(10.44)        // 输出 11

Math.floor(10.44)       // 输出 10
Math.floor(10.55)       // 输出 10

Math.round(10.44)       // 输出 10
Math.round(10.55)       // 输出 11
```

## 随机数方法

`Math.random()`方法返回一个0到1的随机数。
```js
Math.random()           // 输出 0.30080152815794414
Math.random()           // 输出 0.678198864070499
```
## 其他方法
Math 拥有很多方法例如：绝对值，弦切值，平方解方，幂函数等
```js
// 绝对值
Math.abs(-0)            // 输出 0
Math.abs(-5)            // 输出 5
// 解平方
Math.aqrt(5)            // 输出 2.23606797749979
// 参数都是指的“弧度”而非“角度”，弧度的计算公式为： 2*PI/360*角度；返回值在 -1.0 到 1.0 之间
// 弦切函数,象限中 sin=y/r, cos=x/r, tan=y/x, 
// 所以 y=Math.sin(2*PI/360*角度)*r, x=Math.cos(2*PI/360*角度)*r.
Math.sin(2*Math.PI/360*30)   // 输出 0.49999999999999994
Math.cos(2*Math.PI/360*30)   // 输出 0.8660254037844387
Math.tan(2*Math.PI/360*30)   // 输出 0.5773502691896257

// 假设一个圆的圆心坐标是(a,b)，半径为r，则圆上每个点的
// X坐标=a + Math.sin(2*Math.PI / 360) * r ；
// Y坐标=b + Math.cos(2*Math.PI / 360) * r ；

//如何求时钟的秒针转动一圈的轨迹？ 假设秒针的初始值（起点）为12点钟方向，圆心的坐标为（a,b)。
//解决思路：一分钟为60秒，一个圆为360°，所以平均每秒的转动角度为 360°/60 = 6°；
for(var times=0; times<60; times++) {
    var hudu = (2*Math.PI / 360) * 6 * times;
    var X = a + Math.sin(hudu) * r;
    var Y = b - Math.cos(hudu) * r    //  注意此处是“-”号，因为我们要得到的Y是相对于（0,0）而言的。
}
```