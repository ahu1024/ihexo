---
title: Canvas输出图片文件
tags:
  - Canvas
date: 2018-03-30 17:03:21
updated: 2018-03-30 17:03:21
---

> HTML5 Canvas 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成.Canvas 标签只是图形容器，您必须使用脚本来绘制图形。你可以通过多种方法使用 Canvas 绘制路径,盒、圆、字符以及添加图像。下面主要讲的是如何保存已经绘制在Canvas 里的图像.
...................................................................................................

## HTMLCanvasElement.toDataURL()

HTMLCanvasElement.toDataURL() 方法返回一个包含图片展示的 data URI 。可以使用 type 参数其类型，默认为 PNG 格式。图片的分辨率为96dpi。
- 如果画布的高度或宽度是0，那么会返回字符串“data:,”。
- 如果传入的类型非“image/png”，但是返回的值以“data:image/png”开头，那么该传入的类型是不支持的。
- Chrome支持“image/webp”类型。
- 返回值包含 data URI 的DOMString。

语法：
> canvas.toDataURL(type, encoderOptions);

参数：
- type 可选 图片格式，默认为 image/png
- encoderOptions 可选 在指定图片格式为 image/jpeg 或 image/webp的情况下，可以从 0 到 1 的区间内选择图片的质量。如果超出取值范围，将会使用默认值 0.92。其他参数会被忽略。

示例：
```
<canvas id="canvas" width="5" height="5"></canvas>
var canvas = document.getElementById("canvas");
var fullQuality = canvas.toDataURL("image/jpeg", 1.0);
console.log(fullQuality);
// data:image/jpeg;base64,/9j/4AAQSkZJRgABAQ...9oADAMBAAIRAxEAPwD/AD/6AP/Z"

```

兼容： IE 9+

## HTMLCanvasElement.toBlob()

HTMLCanvasElement.toBlob() 方法创造Blob对象，用以展示canvas上的图片；这个图片文件可以被缓存或保存到本地，由用户代理端自行决定。如不特别指明，图片的类型默认为 image/png，分辨率为96dpi。无返回值。

语法:
> void canvas.toBlob(callback, type, encoderOptions);

参数:
- callback 回调函数，可获得一个单独的Blob对象参数。
- type 可选 DOMString类型，指定图片格式，默认格式为image/png。
- encoderOptions 可选 Number类型，值在0与1之间，当请求图片格式为image/jpeg或者image/webp时用来指定图片展示质量。如果这个参数的值不在指定类型与范围之内，则使用默认值，其余参数将被忽略。

示例:
```
<canvas id="canvas" width="5" height="5"></canvas>
var canvas = document.getElementById("canvas");

canvas.toBlob(function(blob) {
  var newImg = document.createElement("img"),
      url = URL.createObjectURL(blob);

  newImg.onload = function() {
    // no longer need to read the blob so it's revoked-不再需要读取这个数据块，所以它被撤销了。
    URL.revokeObjectURL(url);
  };

  newImg.src = url;
  document.body.appendChild(newImg);
}, "image/jpeg", 0.95);

```

Polyfill:

A low performance polyfill based on toDataURL.-低性能 polyfill 基于 toDataURL

```
if (!HTMLCanvasElement.prototype.toBlob) {
 Object.defineProperty(HTMLCanvasElement.prototype, 'toBlob', {
  value: function (callback, type, quality) {

    var binStr = atob( this.toDataURL(type, quality).split(',')[1] ),
        len = binStr.length,
        arr = new Uint8Array(len);

    for (var i=0; i<len; i++ ) {
     arr[i] = binStr.charCodeAt(i);
    }

    callback( new Blob( [arr], {type: type || 'image/png'} ) );
  }
 });
}
```
原生Blob兼容： Chorme 50+、 IE 10+ 、Safari false

## 参考资料
[HTMLCanvasElement.toDataURL()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL)
[HTMLCanvasElement.toBlob()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL)
[ DataURL与File,Blob,canvas对象之间的互相转换的Javascript](http://blog.csdn.net/cuixiping/article/details/45932793)

