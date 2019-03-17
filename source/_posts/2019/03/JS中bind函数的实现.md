---
title: JS中bind函数的实现
tags:
  - bind
categories:
  - javascript
date: 2019-03-10 16:24:24
---
bind函数指定了返回值函数的this指向，同时实现柯里化功能。

```js
Function.prototype.mybind = function(ctx，...bindArgs) {
    if (typeof this != "function") {
        throw new TypeError("...");
    }
    var self = this;
    return (...args) => {
        self.apply(ctx, bindArgs.concat(args))
    }
}
```

