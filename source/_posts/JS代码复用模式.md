---
title: JS代码复用模式
tags:
  - JavaScript
  - 继承
date: 2018-04-21 11:10:30
updated: 2018-04-21 11:10:30
---

> 复用是一项非常重要的生活技能，因为生命是有限的，无意义的重复等于浪费生命。作为一个程序开发者，代码的复用既是一种能力，也是对积极生活的一种态度。那么JS 在代码复用方面都有哪些方法？
> ...................................................................................................

### 构造模式

构造函数与普通函数的唯一区别在于调用方式不同（构造函数首字母大写只是惯例），任何函数都可以用`new`关键字来作为构造函数调用(构造函数 = new + 普通函数)。

```js
function Parent() {
  this.name = "jim";
  this.say = function() {
    console.log(this.name);
  };
  console.log(this.name);
}
Parent(); // 输出 jim
console.log(Parent); // 输出 Parent (){/* 函数体-略 */}

var child1 = new Parent(); // 输出 jim 构造函数创建 child1 对象(解析执行)
var child2 = new Parent(); // 输出 jim 构造函数创建 child2 对象(解析执行)

console.log(child1); // 输出 Parent {name: "jim", say: ƒ ()}
console.log(child1.say); // 输出 ƒ () {/* 函数体-略 */}

child1.say(); // 输出 jim
child2.say(); // 输出 jim

console.log(child1.name); // 输出 jim (child1 继承了 Parent name)
console.log(child2.name); // 输出 jim (child2 继承了 Parent name)

child1.name = "tom1"; // 修改 child 的 name 属性
child2.name = "tom2"; // 修改 child 的 name 属性

child1.say(); // 输出 tom1（说明 child 本地实例化了name属性 ）
child2.say(); // 输出 tom2（说明 child 本地实例化了name属性 ）
console.log(child1.name); // 输出 tom1（说明 child 本地实例化了name属性 ）
console.log(child2.name); // 输出 tom2（说明 child 本地实例化了name属性 ）

delete child1.name; // 删除 child1 的 name 属性
delete child2.name; // 删除 child2 的 name 属性

console.log(child1.name); // 输出 undefined（说明 child1 本地实例化name属性已删除 ）
console.log(child2.name); // 输出 undefined（说明 child2 本地实例化name属性已删除 ）

Parent(); // 输出 jim (说明构造函数属性 和 构造对象属性 没有关系)
```

**缺点：无法复用父对象属性方法，当子对象数量变多，反复使用 new 重新创建父对象.**

### 原型模式

我们知道所有引用类型都是 Object,也就是说引用类型的原型是 Object,他们是一个继承的关系。另外，原型的属性可以自定义。

```js
function fn() {
  this.keyThis = ["fnThisValue"];
}
// name: "fn" prototype: {constructor: fn()} __proto__: Object
// 函数名是 fn
// 函数 prototype 指向一个对象，该对象的属性constructor 指向函数自身
// 函数 __proto__ 指向 Object(重点 __proto__ 是一个原型引用指针，指向父级原型)
// 此时fn 未执行， this 虽然指向window , 但是 keyThis 并未声明和赋值

// 以上是 JS 内部已经实现好的，下面我们来自定义一个原型属性
fn.prototype.keyProto = ["fnProtoValue"];
console.log(fn.prototype);
// 输出 {keyProto: ["fnProtoValue"], constructor: fn(),__proto__: Object}

var foo = new fn(); // fn() 执行， this指向window,key1声明和赋值
console.log(foo);
// 输出
// fn{
//    keyThis:["fooThisValue"],
//    __proto__:{ keyProto: ["fnProtoValue"], constructor: fn(), __proto__: Object}
// }
// foo 仅仅是一个构造对象（重点对象没有原型属性），原型引用指针__proto__指向 fn 的原型
// 原型链 就是 __proto__:{__proto__:{···}}

console.log(foo.keyThis); // 输出 ["fooThisValue"]
console.log(foo.keyProto); // 输出 ["fnProtoValue"]

foo.keyThis.push("fooThis");
foo.keyProto.push("fooProto");

console.log(foo);
// 输出
// fn{
//    keyThis:["fooThisValue", "fooThis"],
//    __proto__:{ keyProto: ["fnProtoValue", "fooThis"], constructor: fn(), __proto__: Object}
// }
// foo 的原型属性竟然被修改了，这应该不是我们想要的（小本本记下来）,所以父级常量最好用 this 来定义

console.log(fn.prototype);
// 输出{ keyProto: ["fnProtoValue", "fooThis"], constructor: fn(), __proto__: Object}
```

**缺点：虽然复用父对象属性方法，当子对象数量变多，反复使用 new 重新创建父对象.**

### 借用模式

在 [JS 基础数据类型操作系列（四）函数](http://peichenhu.cn/2018/04/20/JS%E5%9F%BA%E7%A1%80%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E6%93%8D%E4%BD%9C%E7%B3%BB%E5%88%97%EF%BC%88%E5%9B%9B%EF%BC%89%E5%87%BD%E6%95%B0/) 中，我们介绍了 call,apply 和 bind 的函数作用域借用操作，这也是一种代码复用的好方法。

```js
function Parent() {
  this.keyThis = ["fnThisValue"];
}
Parent.prototype.keyProto = ["fnProtoValue"];
function Child() {
  Parent.call(this);
  console.log(this.keyThis); // 输出 ["fnThisValue"]
  console.log(this.keyProto); // 输出 undefined
}
Child();
// 这种借用只能够针对 this 绑定的属性方法起作用。

var jim = new Child();
console.log(jim.keyThis); // 输出 ["fnThisValue"]
console.log(jim.keyProto); // 输出 undefined
// 这种借用只能够针对 this 绑定的属性方法起作用。
```

### 代理模式

```js
function inherit(parent, child) {
  var F = function() {};
  F.prototype = parent.prototype;
  child.prototype = new F();
  child.prototype.constructor = child;
}

function Parent() {
  this.keyThis = ["fnThisValue"];
}
Parent.prototype.keyProto = ["fnProtoValue"];

function Child() {}
inherit(Parent, Child);

var jim = new Child();
console.log(jim.keyThis); // 输出 undefined
console.log(jim.keyProto); // 输出 ["fnProtoValue"]
```

**缺点：只是代理了原型**

### 标准模式

在 ES 5 中，提供了`Object.create()`方法来实现原型构造继承（语法糖）。
`Object.create()`方法创建一个新对象，使用现有的对象来提供新创建的对象的`__proto__`

> 语法 ：Object.create(proto, [propertiesObject]) 。

第二个可选参数是 null 或一个对象，添加到新创建对象的自定义可枚举属性，对应 Object.defineProperties()的第二个参数。

```js
function Parent() {}
Parent.prototype.keyProto = ["fnProtoValue"];

var jim = Object.create(Parent, {
  key: { value: "val" }
});

console.log(jim); // 输出 Function {key: "val",__proto__: Parent()}
jim.hasOwnProperty("key");


var Fn = {
    key:"value"
}
Object.create(Fn)
// {__proto__:{ key:"value"}}
```

### 克隆模式

通过复制属性来实现继承

#### 浅克隆

简单对象，单层克隆

```js
function extend(parent, child) {
  var i;
  child = child || {};
  for (i in parent) {
    if (parent.hasOwnProperty(i)) {
      child[i] = parent[i]; // 这里只是引用， 并非实例化
    }
  }
  return child;
}

var Parent = {
    key:"value",
    arr:[1,2,3,4],
    obj:{
        key:"value",
        arr:[1,2,3,4],
    }
}
var kid = extend(Parent)
kid.arr.push(4);
console.log(Parent.arr)  // 输出 [1,2,3,4,4]

```

#### 深克隆

复杂对象，递归克隆

```js
function extendDeep(parent, child) {
  var i,
    toStr = Object.prototype.toString,
    astr = "[object Array]";
  child = child || {};
  for (i in parent) {
    if (parent.hasOwnProperty(i)) {
      if (typeof parent[i] === "object") {
        child[i] = toStr.call(parent[i]) === astr ? [] : {};
        arguments.callee(parent[i], child[i]);
      } else {
        child[i] = parent[i];
      }
    }
  }
  return child;
}
var Parent = {
    key:"value",
    arr:[1,2,3,4],
    obj:{
        key:"value",
        arr:[1,2,3,4],
    }
}
var kid = extendDeep(Parent)
kid.arr.push(4);
console.log(Parent.arr)  // 输出 [1,2,3,4]
```

**缺点：针对的是对象，不是函数，当然对象用这个是最好的**

### 总结

综上了解，我们想要一个既可以继承`this`属性,又可以继承`prototype`属性的方法。继承`this`属性最好用的是借用模式，继承`prototype`属性最好用的是`Object.create()`标准模式。

```js
function parent() {
  this.money = 1000;
}
parent.prototype.say = function(money) {
  console.log("I have " + (this.money + money));
}

function inherit(parent,childParams){
    function Child() {
        parent.call(this);      // 借用 父级 this 属性
    }
    childParams = childParams || {}; // 定义额外参数
    Child.prototype = Object.create(parent.prototype,childParams);
    // parent.prototype 指向原型对象parent Prototype
    // Object.create(parent.prototype)
    // 输出 {__proto__:{ say:ƒ (money),constructor:ƒ parent(), __proto__:Object}}
    Child.prototype.constructor = Child; // 原型的构造函数应该永远指向自身
    return new Child()
}

var jim = inherit(parent);
var tom = inherit(parent,{key:{value:500}});
jim.say(100);   //输出 I have 1100
tom.say(500);   //输出 I have 1100
tom.key         //输出 500
```
