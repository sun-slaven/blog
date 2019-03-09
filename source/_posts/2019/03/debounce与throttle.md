---
title: debounce与throttle
tags:
  - debounce
  - throttle
categories:
  - javascript
date: 2019-03-06 21:34:27
---
防抖和节流是比较常用的一种性能优化函数。但是这两者的微弱区别导致很多同学容易混淆。

### 给个场景
```
debounce
假设你正在乘电梯上楼，当电梯门关闭之前发现有人也要乘电梯，礼貌起见，你会按下开门开关，然后等他进电梯； 
如果在电梯门关闭之前，又有人来了，你会继续开门；
这样一直进行下去，你可能需要等待几分钟，最终没人进电梯了，才会关闭电梯门，然后上楼。
```
所以debounce的作用是，当调用动作触发一段时间后，才会执行该动作，若在这段时间间隔内又调用此动作则将重新计算时间间隔

```
throttle
假设你正在乘电梯上楼，当电梯门关闭之前发现有人也要乘电梯，礼貌起见，你会按下开门开关，然后等他进电梯；  
但是，你是个没耐心的人，你最多只会等待电梯停留一分钟；
在这一分钟内，你会开门让别人进来，但是过了一分钟之后，你就会关门，让电梯上楼。
```
所以throttle的作用是，预先设定一个执行周期，当调用动作的时刻大于等于执行周期则执行该动作，然后进入下一个新的时间周期。

### 简单实现
##### debounce
1. debounce函数会通过闭包维护一个timer
2. 当同一action在delay的时间间隔内再次触发，则清理timer，然后重新设置timer
```js
function debounce(fn, delay) {
  var timer = null;

  return function() {
    var self = this;
    var args = arguments;
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(self, args);
    }, delay);
  }
}

window.onresize = debounce(resizeHandler, 300);

```

##### throttle
throttle跟debounce的最大不同就是，throttle会有一个阀值，当到达阀值的时候action必定会执行一次
```js
function throttle(fn, delay) {
  var start = 0;

  return function() {
    var now = Date.now();

    if (now - start > delay) {
      fn.apply(this, arguments);
      start = now;
    }

  }
}
```