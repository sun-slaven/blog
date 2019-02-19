---
title: javascript原型
tags:
  - prototype
categories:
  - javascript
date: 2017-02-19 17:24:52
---
function A(){};

var a = new A();



a.__proto__ === A.prototype

a.prototype //undefined



A.__proto__ ===Function.prototype

A.prototype// object空对象  原型链从此处赋值实现

![](http://7xs8pt.com1.z0.glb.clouddn.com/javascript%E5%8E%9F%E5%9E%8B%E5%9B%BE.png)
