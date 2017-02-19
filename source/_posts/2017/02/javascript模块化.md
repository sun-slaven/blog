---
title: javascript模块化
tags:
  - 模块化
categories:
  - javascript
date: 2017-02-19 17:27:47
---
### 1. AMD (老大) - RequireJs
```
// 定义模块 myModule.js
define(['dependency'], function(){
    var name = 'Byron';

    function printName(){
        console.log(name);
    }

    return {
        printName: printName
    };
});

// 加载模块
require(['myModule'], function (my){
　  my.printName();
});
```
### 2. CMD (小三) SeaJs（浏览器端）
CMD是玉伯在推出seajs的时候提出的。遵循CommonJs规范，只是在浏览器端的实现。
```
//CMD
define(function(require,exports,module){
    //此处如果需要某XX模块，可以引入
    var xx=require('XX');
});
```
### 3.  CommonJs（服务器端)
就是nodejs使用的那套，
```
//模块定义 myModel.js
var name = 'Byron';
function printName(){
    console.log(name);
}
function printFullName(firstName){
    console.log(firstName + name);
}

module.exports = {
    printName: printName,
    printFullName: printFullName
}

//加载模块
var nameModule = require('./myModel.js');
nameModule.printName();
```

总结：

Commonjs规范推崇：
 1. 一个文件就是一个模块，
 2. 依赖就近，用的时候再require。

AMD则相反，定义模块的时候需要制定依赖模块，并以形参的方式引入factory中。
