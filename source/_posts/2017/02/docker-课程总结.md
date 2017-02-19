---
title: docker 课程总结
tags:
  - null
categories:
  - Docker
date: 2017-02-19 19:35:09
---
nginx -g "daemon off;"  //前台启动nginx

docker run -d --name [container_name] [image_id]  bash

supervisor要求所有的服务都是以前台运行，不能以后台服务方式运行。

dockerfile 换行结尾： '\'

COPY [和dockerfile平级或子级的文件]  [docker path]

ADD 更强大，包含COPY命令功能。会自动解压tar 到target目录

VOLUME 设置挂载点，将本机的一些目录挂载到docker里

    VOLUME [docker挂载路径] //只有一个path，主机的path需要在run时-v指定

docker run -v 指定挂载点 // $(pwd) 指定返回全局路径

docker-compose 指定volumes_from: [container_name], 实现共享卷。container_name可以不处于运行中

docker cp [容器名]:[容器里文件路径]  [目标容器]

link形式，redis只对node容器可见,会自动在host里添加一层映射.

docker run -d --link 容器名:alias名     在启动node容器时，-- link redis容器 只能单向, redis里ping不了node容器。



### docker 操作network:
```
docker network create -d [bridge] [network_name] 创建一个network_name，方式为bridge。
docker network ls 查看当前所有的网络
docker network inspect [network_name] 查看该网络的详细信息。
docker network connect my-net 容器名（容器加入网络）
docker network disconnect my-net 容器名（容器脱离网络） 
docker network rm my-net（删除网络）
docker run --network=my-net …（容器运行时设置网络）
```
