---
title: JS中实现一个浅/深拷贝
tags:
  - 深拷贝
categories:
  - javascript
date: 2019-03-10 16:23:32
---
## 前言
每次都被问这种问题，其实也没什么难度，但是想要回答的比较全面还是需要花点时间总结一下的。本质上就是要理解js的对象存储特性。

## 浅拷贝
1. 使用Object.assign
2. 使用展开运算符 ...
3. 对象属性遍历赋值
## 深拷贝
#### 1. 序列化+反序列化
```js
JSON.parse(JSON.stringify(object))
```
局限性：
* 会忽略 undefined与symbol
* 不能序列化函数
* 不能解决循环引用的对象
#### 2. 对象属性递归遍历赋值
以下实现能实现对object以及array的深拷贝。
```js
function cloneDeep2(source) {

    if (!isObject(source)) return source; // 非对象返回自身

    var target = Array.isArray(source) ? [] : {};
    for(var key in source) {
        if (Object.prototype.hasOwnProperty.call(source, key)) {
            if (isObject(source[key])) {
                target[key] = cloneDeep2(source[key]); // 注意这里
            } else {
                target[key] = source[key];
            }
        }
    }
    return target;
}
```
##### a.如何解决循环引用的问题？
使用hash表，循环检测，我们设置一个数组或者哈希表存储已拷贝过的对象，当检测到当前对象已存在于哈希表中时，取出该值并返回即可。本质上就是程序设定一个返回条件
```js
function cloneDeep3(source, hash = new WeakMap()) {

    if (!isObject(source)) return source; 
    if (hash.has(source)) return hash.get(source); // 新增代码，查哈希表

    var target = Array.isArray(source) ? [] : {};
    hash.set(source, target); // 新增代码，哈希表设值

    for(var key in source) {
        if (Object.prototype.hasOwnProperty.call(source, key)) {
            if (isObject(source[key])) {
                target[key] = cloneDeep3(source[key], hash); // 新增代码，传入哈希表
            } else {
                target[key] = source[key];
            }
        }
    }
    return target;
}
```
##### b.如何拷贝 Symbol 类型?
首先需要检测出事symbol类型
* Object.getOwnPropertySymbols(...)
* Reflect.ownKeys(...)，该方法相当于Object.getOwnPropertyNames(target).concat(Object.getOwnPropertySymbols(target))

使用方法一的最终代码：
```js
function cloneDeep4(source, hash = new WeakMap()) {

    if (!isObject(source)) return source; 
    if (hash.has(source)) return hash.get(source); 

    let target = Array.isArray(source) ? [] : {};
    hash.set(source, target);

    // ============= 新增代码
    let symKeys = Object.getOwnPropertySymbols(source); // 查找
    if (symKeys.length) { // 查找成功    
        symKeys.forEach(symKey => {
            if (isObject(source[symKey])) {
                target[symKey] = cloneDeep4(source[symKey], hash); 
            } else {
                target[symKey] = source[symKey];
            }    
        });
    }
    // =============

    for(let key in source) {
        if (Object.prototype.hasOwnProperty.call(source, key)) {
            if (isObject(source[key])) {
                target[key] = cloneDeep4(source[key], hash); 
            } else {
                target[key] = source[key];
            }
        }
    }
    return target;
}
```
使用方法二的最终代码:
```js
function cloneDeep4(source, hash = new WeakMap()) {

    if (!isObject(source)) return source; 
    if (hash.has(source)) return hash.get(source); 

    let target = Array.isArray(source) ? [...source] : { ...source }; // 改动 1
    hash.set(source, target);

      Reflect.ownKeys(target).forEach(key => { // 改动 2
        if (isObject(source[key])) {
            target[key] = cloneDeep4(source[key], hash); 
        } else {
            target[key] = source[key];
        }  
      });
    return target;
}
```