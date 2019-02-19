---
title: '关于hibernate通过注解方式自动生成表时字段的顺序问题'
tags:
- Hibernate
categories:
- java
date: 2015-06-06 20:18:45
---
今天在使用hibernate3.0的annotation方式自动生成表时，发现生成表后总是插入不了记录（该记录按照entity实体的field顺序），仔细观察自动生成的表发现新表的字段顺序竟然和entity映射的field顺序不一致！所以插不进去。在网上百度了一下，发现这是hibernate自身的一个错误，通过xml方式配置不会产生这个问题，但是以annotation方式自动生成的表会默认按照entity的field的首字母顺序作为新表的字段！

详细解决方案看[点击打开链接](http://www.cnblogs.com/eggbucket/archive/2013/03/05/2943727.html)
