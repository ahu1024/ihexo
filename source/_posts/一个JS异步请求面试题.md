---
title: 一个JS异步请求面试题
tags:
  - JavaScript
  - Async
  - Promise
date: 2018-04-15 00:57:09
updated: 2018-04-15 00:57:09
---

> JavaScript语言将任务的执行模式可以分成两种：同步（Synchronous）和异步（Asychronous）。“同步模式”就是一个任务完成之后，后边跟着一个任务接着执行；程序的执行顺序和排列顺序是一直的；”异步模式”则完全不同，每一个任务都有一个或者多个回调函数（callback），前一个任务结束的时候，不是执行下一个任务，二十执行回调函数，后一个任务则是不等前一个任务结束就执行，所以程序的执行顺序与任务顺序不一致的，异步的。
...................................................................................................
“异步模式”一共有4种方法，这4种方法可以写出结构更合理，性能更出色，维护更方便的js代码。这四种模式分别为：`回调函数（callback）``事件监听（Listener）``观察者模式``promise对象`,具体的不再多说先看题：

{% img https://github.com/pch1024/doc/blob/master/images/async.jpg?raw=true %}

下面是我根据题干定义的数据：

```js
const list = [{
        name: 'a',type: '1',id: "1",pid: '',
        ajax:()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 2000') }, 2000)})
    },{
        name: 'a',type: '2',id: "2",pid: '1',
        ajax: ()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 4000') }, 4000)})
    },{
        name: 'a',type: '2',id: "1",pid: '',
        ajax: ()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 7000') }, 7000)})
    },{
        name: 'b',type: '1',id: "1",pid: '',
        ajax: ()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 10000') }, 10000)})
    },{
        name: 'c',type: '2',id: "4",pid: '3',
        ajax: ()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 30000') }, 30000)})
    },{
        name: 'b',type: '2',id: "3",pid: '2',
        ajax: ()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 500') }, 500)})
    },{
        name: 'a',type: '3',id: "1",pid: '',
        ajax: ()=> new Promise(function(resolve,reject){setTimeout( () => { resolve('hello 6000') }, 6000)})
    }
];
```

- 接下来就是要根据已知条件， 将数据进行分组和排序

```js
const AList = list.filter(item => item.type === '1')
const BList = list.filter(item => item.type === '2')
// 先找一个存在父子关系的
const tmpBList = BList.filter(item => item.pid !== '');
const tmp2BList = loopUp([tmpBList[0]]);
const sortBList = loopDown(tmp2BList);
// 遍历无序集合,找父链
function loopUp(list) {
    let i = 0,
        tmp = list;
    while (i < BList.length) {
        if (tmp[0].pid === BList[i].id) {
            // 插入到有序集合第一位
            tmp.unshift(BList[i]);
            loopUp(tmp)
        } else {
            i++;
        }
    }
    return tmp;
}

// 遍历无序集合,找子链
function loopDown(list) {
    let i = 0,
        tmp = list;
    while (i < BList.length) {
        if (tmp[tmp.length - 1].id === BList[i].pid) {
            // 插入到有序集合第一位
            tmp.push(BList[i]);
            loopDown(tmp)
        } else {
            i++;
        }
    }
    return tmp;
}

// 筛选出独立元素
const unsortBList = [];
(BList.filter(item => item.pid === '')).forEach(function (i) {
    let status = true;
    BList.forEach(function (j) {
        if (i.id === j.pid) {
            status = false;
        }
    })
    if (status) unsortBList.push(i);
})

const CList = list.filter(item => item.type === '3')

// 最终的数据 已排序
const resultList = AList.concat(unsortBList, sortBList, CList)
```

- 当数据全部整理好，剩下的就是要根据数据来完成异步请求了。

```js

asyncLoop(resultList,0)

function asyncLoop(list,index){
    if(index<list.length){
        list[index].ajax()
        .then(function (result) {
            console.log('执行序列号:' + index);
            console.log('成功：' + result);
            console.log((new Date).getSeconds()+"秒");
            asyncLoop(resultList,++index)
        }).catch(function (reason) {
            console.log('失败：' + reason);
        });
    }
}

```

- 完整的代码运行实例如下：

<a class="jsbin-embed" href="http://jsbin.com/bunewid/1/embed?js,console">JS Bin on jsbin.com</a>
<script src="http://static.jsbin.com/js/embed.min.js?4.1.4"></script>

