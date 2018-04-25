---
title: CSS 中 BEM 命名规范
tags:
  - CSS
  - BEM
date: 2018-04-25 16:05:17
updated: 2018-04-25 16:05:17
---

> BEM 的意思就是块（block）、元素（element）、修饰符（modifier），是由 Yandex 团队提出的一种 CSS Class 命名方法。在某些方面，BEM 与 OOP 类似 - 这是一种用代码描述现实的方式，具有一系列模式，以及关于程序实体的思考方式，而不管所用的编程语言如何。
> ...................................................................................................

## 相关资料 (侵删)

[GET BEM](http://getbem.com/introduction/)
[知乎 BEM 讨论](https://www.zhihu.com/question/21935157)
[BEM 原则](https://coding.smashingmagazine.com/2012/04/a-new-front-end-methodology-bem/)
以下内容是个人对于规范理解所做出的适合自己的约束规则（可能与官方规范不尽相同）

## B（block）

一个块是一个独立的实体，是一个应用程序的“构建块”。块可以是简单的也可以是复合的（包含其他块）。

* 块名称在项目中必须是唯一的，才能明确指定正在描述的块。只有同一个块的实例可以具有相同的名称。在这种情况下，我们可以说一个块在页面上出现两次（或 3,4 次，等等）。

## E （element）

一个元件（属性、元素）是执行特定功能的块的一部分。元素是依赖于上下文的：它们只在它们所属的块的上下文中才有意义。

* 元素可以重复多次。
* 元素名称在块的范围内必须是唯一的。

## B+E

块和元素是描述页面和模板的方式，构成页面内容。除了简单地出现在网页上，标识它的关键字和排列方式也很重要。最终我们将会得到类似下面的 树形（tree）结构：

```html
<div class="shopCart">
    <div class="shopCart-title">
    </div>
    <div class="shopCart-items">
        <div class="product">
            <p class="product-title"></p>
            <p class="product-price"></p>
        </div>
    </div>
    <div class="shopCart-items selected">
        <div class="product">
            <p class="product-title"></p>
            <p class="product-price"></p>
        </div>
    </div>
</div>
```

或者一种 JSON 对象模式：

```js
{
  block: 'shopCart',
  content: [
    {
        elem: 'shopCart-title',
    },
    {
        elem: 'shopCart-items',
        content:[
            {
                block: 'product',
                content: [
                    {
                        elem: 'product-title',
                    },
                    {
                        elem: 'product-price',
                    }
                ]
            }
        ]
    }
}
```

对应CSS:

```css

.shopCart{}
.shopCart-title{}
.shopCart-items{}
.shopCart-items.selected{}

.product{}
.product-title{}
.product-price{}
/**
关键字采用 小驼峰 命名规范
B-E 从属关系以 连字符 分隔
避免出现 链式选择器 和 标签选择器

*/
```

**终极目标是使用 BEM Tree 来生成直接生成真实 DOM 结构**

## M (modifier)

元素和块的修饰符。当有非常类似于现有的块，但外观或行为稍有改变时，以复用为前提，应该添加一个对元素和块的修饰符来完成特殊化操作。

* 在 BEM 树中，修饰符是描述块或元素的实体的属性。
* 修饰符是块或元素的附加 CSS 类。

## 补充

块（或元素）必须具有可以在 CSS 规则中使用的唯一“名称”（CSS 类）。不能在 CSS 选择器（.menu td）中使用 HTML 元素，因为这样的选择器本质上不是上下文无关的。级联选择器应避免多个块。
