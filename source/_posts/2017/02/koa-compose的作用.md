---
title: koa-compose的作用
tags:
  - compose
  - koa
categories:
  - Nodejs
date: 2017-02-19 17:16:47
---
compose是koa运行中间件的发动机，作用是将所有的中间件以v型方式自动执行。
```
function compose(middleware){
        return function *(next){
                if (!next) next = noop();//默认置空next
                var i = middleware.length;
                while (i--) {
                    next = middleware[i].call(this, next);//每个中间件的参数就是此处的next，即下一个中间件
                }
                return yield *next;//经过while循环，此处的next作为第一个中间件的指针
        }
 }
 ```
 ---
参考：
http://cnodejs.org/topic/5780e12e69d72f545483ca69
