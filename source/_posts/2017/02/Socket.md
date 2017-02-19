---
title: Socket
tags:
  - socket
categories:
  - 杂项
date: 2017-02-19 19:56:23
---
socket在不同场景下有不同的含义。

1. TCP Socket（socket编程，因特网套接字）：本质是一个API，由TCP/IP抽象出的一层即socket处理层。此时的socket使用 host:port形式唯一标识<font color=#FF4500 size=3 face="黑体" bgcolor=#0099ff>网络上的</font>进程，实现不同主机之间的进程通信，基本所有使用TCP协议的程序都是使用的此种socket。

2. Unix域套接字（IPC socket）：并不是一个实际的协议族（接字可用于同一目的，<font color=#0099ff size=3 face="黑体" bgcolor=#0099ff>但UNIX域套接字的效率更高。UNIX域套接字仅仅复制数据</font>；它们并不执行协议处理，不需要添加或删除网络报头，无需计算检验和，不要产生顺序号，无需发送确认报文），而是在单个主机上执行客户/服务器通信的一种方法，用于实现<font color=#FF4500 size=3 face="黑体" bgcolor=#0099ff>同一主机</font>上的多个进程通信。使用<font color=#FF4500 size=3 face="黑体" bgcolor=#0099ff>.sock文件地址</font>作为自己的身份，这种通信方式是发生在系统内核里而不会在网络里传播。
当web端（node）使用curl调用后台java的接口时，默认是一次请求后就断开连接了，curl并非不支持http1.1,而是客户端自己请求完后就断开了（？）。想要减少请求开销时，就要想法保持连接（keep-alive），像浏览器是默认支持的。保持连接，可以通过nginx转发，因为nginx的通信功能足够完善，它能通过配置实现长连接。所以现在的问题就是应用的请求如何通过nginx来发？这无疑使用Unix域协议是最合适的，因为这种方式并不是网络传播而是内核通信（Unix域套接字往往比通信两端位于同一主机的TCP套接字快出一倍）。
nginx配置监听 域协议请求，然后转发。
```
    1. //socket.conf
    2. server {
    3. listen unix:/tmp/backend_semantic.sock;//一般都放在/tmp目录下，由相应的模块自动生成
    4. set $backend_service http://{{SEMANTIC_SERVER}};
    5. location / {
    6. proxy_pass $backend_service;
    7. proxy_http_version 1.1;
    8. proxy_set_header Connection "";
    9. proxy_set_header Host "{{SEMANTIC_SERVER}}";
    10. }
    11. }
```
---

参考：
https://blog.linuxeye.com/364.html
