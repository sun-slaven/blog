---
title: volume以及volume_from
tags:
  - volume
  - volume_from
categories:
  - Docker
date: 2017-02-19 19:30:58
---
#### volume来源：
1. docker run -v 命令
2. dockerfile文件的 VOLUME配置
3. docker-compose 文件 volumes配置

作用：创建挂载点

docker run时候以及docker-compose 文件 volumes配置指定host和容器的位置映射，而dockerfile中的VOLUME配置只能指定容器的位置映射，若在创建容器时候不指定 -v ，则默认以host的/var/lib/docker路径挂载到配置的容器位置。dockerfile中的VOLUME配置可以不写

#### volume from来源：

1. docker run --volume-from [container_name]
2. docker-compose 文件 volume-from 配置

作用：授权一个容器访问[container_name]的Volume路径（单向访问）。一般[container_name]作为数据存储卷使用，不运行相应的应用程序。[container_name]必须要有volume映射。
[container_name]容器不管有没有运行都会生效。
