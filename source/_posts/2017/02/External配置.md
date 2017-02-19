---
title: External配置
tags:
  - Webpack配置
categories:
  - Webpack
date: 2017-02-19 17:05:22
---
External： 指定的依赖不会被webpack解析，但会成为bundle里的依赖。

这句话什么意思？

就是webpack在解析的时候，包加载器（import Vue from 'vue';）加载配置的值（库、第三方插件）时，它不会被打包进入使用包加载器的那个文件中去，也就是vue并不会被被webpack处理。后半句话的意思是，虽然vue没有被打包进webpack的最终文件（/dist/index.bundle.js），但是webpack在解析文件时，外部的闭包函数参数会留有该配置项的值，只要vue被其他方式引入（甚至直接script标签引入）到执行环境，index.bundle.js文件照样可以引用vue。

实例：在lib-components中，webpack.config.js使用了external，webpack.config.test.js注释了external。造成的区别就是，npm run build 时候，dist文件是不含有vue等文件的，而外部npm install lib-components的项目static,require lib-components 时，也是用webpack打包，因为外部的webpack打包了vue，所以lib-components的文件可以直接使用外部的static项目的vue版本。


值是对象，字符串，函数，正则，数组都会被接受：
字符串：一个精确匹配的依赖会变成externals依赖，同一字符串会被用于externals依赖。

对象：如果依赖精确匹配到了对象的一个属性，属性值就会被当作externals依赖。属性值可以包含一个依赖型的前缀，用一个空格隔开。如果属性值为true，则使用该属性名。如果属性值为false，外部测试失败，这个依赖是内部依赖。见下面的例子。

函数：function(context, request, callback(err, result))。函数会在每个依赖中调用。如果结果被传递到回调函数里，这个值就会被像处理对象属性值那样处理。

正则表达式：每个被匹配的依赖都会成为外部依赖。匹配的文本会被用作外部依赖的请求。因为请求是用于生成外部代码钩子的确切代码，如果你匹配到一个cmd的包(比如 ‘../some/package.js’),相反使用外部function的策略。你可以通过callback(null, “require(‘” + request + “’)”引入包，这个包生成module.exports = require(‘../some/package.js’);使用要求在webpack上下文外。

数组：这个表示多个值(递归)
