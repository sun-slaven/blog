---
title: CO的理解、Thunk函数
tags:
  - CO
  - Thunk函数
categories:
  - Nodejs
date: 2017-02-19 17:07:30
---
co精简版只支持yield后面是thunk函数的情况。实际co也支持promise。co精简版只是方便原理的解读。

co精简版：
```
function co(generator) {
  return function(fn) {
        var gen = generator();
        function next(err, result) {
                if(err){
                        return fn(err);
                }
                var step = gen.next(result);
                if (!step.done) {
                        step.value(next);//这里step.value是一个function,即thunk函数里返回的函数，next作为callback
                             保证了co包裹的generator能够不使用yield*就可以递归调用generator里的generator
                } else {
                        fn(null, step.value);//这里将generator的返回值作为yield的返回值返回
                }
        }
        next();
   }
}
```
用法：
```
var co = require('./co');
// wrap the function to thunk
function readFile(filename) {
    return function(callback) {
            require('fs').readFile(filename, 'utf8', callback);
    };
}

co(function * () {
    var file1 = yield readFile('./file/a.txt');
    var file2 = yield readFile('./file/b.txt');

    console.log(file1);
    console.log(file2);
    return 'done';
})(function(err, result) {
    console.log(result)
});
```
会打印出：
```
content in a.txt

content in b.txt

done
```
---

co为什么要返回一个function？

返回一个functoin是为了把一个普通的函数变成thunk（什么是Thunk？<font color=#FF0000 size=3 face="黑体">一个多参数函数里返回单参数的函数版本，且只接受回调函数作为参数<font>）

<font color=#FF4500 size=3 face="黑体">thunk类似promise, 可以把一个函数延后执行，每个thunk函数只有一个且必须是callback回调参数。</font>

这段代码就是将一个普通的nodejs函数转换为thunk：
```
function readFile(filename，encode) {
    return function(callback) {
        require('fs').readFile(filename, encode, callback);
   };
}
```
当你调用readFile(‘a.txt’)的时候并不会去读取文件，它会返回一个function，然后通过这个function去执行：
```
 readFile('a.txt')(function(err,result){})；
 ```
把普通的函数转为thunk是为了配合co的实现（能够被yield），TJ大神写过一个库可以方便地将普通的nodejs函数转换成thunk（https://github.com/visionmedia/node-thunkify）

<font color=#FF4500 size=3 face="黑体">这里的co函数返回一个function(fn)是为了把co函数本身也变成一个thunk，这样就co本身也可以被yield。</font>

---
资源： http://blog.csdn.net/fendouzhe123/article/details/50426156
