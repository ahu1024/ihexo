---
title: JS Util - 常用工具型代码片段
tags:
  - Util
  - JavaScript
date: 2018-05-17 11:37:47
updated: 2018-05-17 11:37:47
---

> 日常工作中时常用的 JavaScript 工具型代码片段，包括对象深拷贝，拖拽，假类型检测，快速排序，快速去重等。
> ..............................................................................................................

## 对象深拷贝

```js
export const DeepClone = obj => {
	if (typeof obj !== 'object') return obj; // 参数类型非对象引用类型直接返回
	let result =
		Object.prototype.toString.call(obj) === '[object Array]' ? [] : {}; // 参数是数组引用类型还是对象引用类型
	for (let key in obj) {
		result[key] =
			typeof obj[key] === 'object' ? DeepClone(obj[key]) : obj[key]; // 值是引用类型进行深层递归，值是值类型直接返回
	}
	return result;
};
```

## 事件监听器

```js
export const eListener = (el, event, callback, capture) => {
	var passiveSupported = false;
	try {
		Object.defineProperty({}, 'passive', {
			get: () => {
				passiveSupported = true;
			}
		});
	} catch (err) {}

	capture = capture || false;
	el.addEventListener(
		event,
		e => {
			callback(e);
			e.preventDefault();
			e.stopPropagation();
		},
		passiveSupported ? { passive: true } : capture
	);
};
```

## 拖拽事件监听器

```js
export const DargDrop = options => {
	let startX, startY, moveX, moveY; // 开始坐标XY,拖拽移动距离XY
	let el = options.el || document; // 目标元素或者文档根节点

	let isMobile = 'ontouchstart' in document; // 检测Touch支持
	let isMousePress = false; // 鼠标点击按压状态
	let isMove = false; // 移动状态

	console.log(isMobile ? 'touch' : 'mouse');

	let TouchEvents = {
		start: isMobile ? 'touchstart' : 'mousedown', // 事件类型，开始
		move: isMobile ? 'touchmove' : 'mousemove', // 事件类型，移动
		end: isMobile ? 'touchend' : 'mouseup' // 事件类型，结束
	};

	eListener(el, TouchEvents.start, e => {
		isMousePress = true; // 开始，鼠标点击按压状态
		e = isMobile ? e.touches[0] : e; // 开始，事件对象
		[startX, startY] = [e.clientX, e.clientY]; // 开始，解构赋值
		options.start(startX, startY, el, e); // 开始，调用start()
	});

	eListener(el, TouchEvents.move, e => {
		isMove = true; // 移动，标记移动状态
		e = isMobile ? e.touches[0] : e; // 移动，事件对象
		[moveX, moveY] = [e.clientX - startX, e.clientY - startY]; // 移动，计算移动距离
		if (!isMobile && isMousePress) {
			// 移动，当使用Mouse并且点击按压式状态
			options.move(moveX, moveY, el, num, e); // 移动，调用move()
		}
		if (isMobile) {
			// 移动，当使用Touch
			options.move(moveX, moveY, el, num, e); // 移动，调用move()
		}
	});

	let _end = () => {
		if (isMove && isMousePress) {
			//结束，当移动状态并且鼠标点击按压状态
			isMove = false; // 重置移动状态
			isMousePress = false; // 重置鼠标点击按压状态
			options.end(moveX, moveY, el, num); // 调用end()
		}
	};
  
	eListener(el, TouchEvents.end, _end);

	// Mouse 兼容处理，解决当鼠标按压滑出目标元素时无法捕捉end,此时监听鼠标滑出目标元素事件leave
	if (!isMobile) {
		eListener(el, 'mouseleave', _end);
	}
};
```
