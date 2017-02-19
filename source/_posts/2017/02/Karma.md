---
title: Karma
tags:
  - Karma
categories:
  - 前端测试
date: 2017-02-19 17:45:56
---
Karma是一个测试环境的 runner, 旨在帮助开发者简单而又快速的进行自动化单元测试。karma 是一个典型的 C/S 程序，包含 client 和 server ，通讯方式基于 Http ，通常情况下，客户端和服务端基本都运行在开发者本地机器上。

![](http://7xs8pt.com1.z0.glb.clouddn.com/karma1.png)

### 1. server

Server 是框架的主要组成部分之一，它内部保存了所有的程序运行状态，比如 client 连接，当前运行的单测文件，根据这些数据状态，它提供了下面几个功能:

* 监听文件
* 与 client 进行通讯
* 向开发者输出测试结果
* 提供 client 端所需的资源文件

注意：连接 server 的 client 浏览器有多种类型，比如 PC，iphone，TV 端等

### 2. client

Client 是测试文件真正运行的地方，比如一个 PC，iphone，tablet 端的浏览器，通常情况下跟 server 是同一个物理机，当然也可以运行在不同的机器，通过 HTTP 来通讯。多个 Client 可以利用 socket.io与一个Server 进行通讯。 执行单测在一个独立的 iframe 中。

![](http://7xs8pt.com1.z0.glb.clouddn.com/karma2.png)

 1. #### Adapter

    是第三方测试框架对应的 karma 适配器，本身不是框架的一部分，是以插件的形式加载到 HTML 里的， 这样就可以保证， 无论什么测试框架，karma 都可以无缝接入， 想要系统适应不同框架的问题，就得提供一套约束出来，想要开发一个适配器，至少得实现 __karma__.start 方法， 这个方法最终会被 manager 来调来， 它是执行本地单测的入口方法。

一般都是karma-xx形式的npm插件

### 3. 使用

karma init 回答一系列问题，生成相应的karma.conf.js文件。

运行：
karma start test/unit/karma.conf.js
