---
title: Promise以及Async/Await的实现原理
tags:
  - Promise
  - Async
categories:
  - javascript
date: 2019-03-10 16:22:16
---
## Promise
https://segmentfault.com/a/1190000016225301#articleHeader3

```js
function Promise(fn) {
    var value = null,
        callbacks = [];  //callbacks为数组，因为可能同时有很多个回调
    this.state = 'pending';
    
    // then方法最好通过扩展原型来定义
    this.then = function (onFulfilled) {
        callbacks.push(onFulfilled);
        return this;
    };

    function resolve(value) {
        callbacks.forEach(function (callback) {
            callback(value);
        });
    }

    fn(resolve);
}
```
## Async

async 函数的实现原理，就是将Generator函数和自动执行器，包装在一个函数里。async本质是一个高阶函数。返回一个Promise的实例，

```js
async function fn(args) {
  // ...此处内容变成generate函数的内容
}

// 等同于

function fn(args) {
  return spawn(function* () {
    // ...
  });
}
```
所有的async函数都可以写成上面的第二种形式，其中的spawn函数就是自动执行器。

下面给出spawn函数的实现
```js
function spawn(genF) {
  return new Promise(function(resolve, reject) {
    const gen = genF();
    function step(nextF) {
      let next; 
      try {
        next = nextF();
      } catch(e) {
        return reject(e);
      }
      if(next.done) {
        return resolve(next.value);
      }
      Promise.resolve(next.value).then(function(v) {
        step(function() { return gen.next(v); });
      }, function(e) {
        step(function() { return gen.throw(e); });
      });
    }
    step(function() { return gen.next(undefined); });
  });
}
```