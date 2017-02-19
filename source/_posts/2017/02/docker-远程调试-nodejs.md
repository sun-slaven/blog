---
title: docker 远程调试 nodejs
tags:
  - 调试
  - nodejs
categories:
  - Docker
date: 2017-02-19 19:33:14
---
暴露 docker container 的5858 端口，然后npm install supervisor -g

执行 supervisor --watch . --debug app.js

然后在webstorm里配置configuration 点击+ 选择nodejs remote debugger
