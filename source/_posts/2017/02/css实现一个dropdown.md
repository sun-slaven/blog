---
title: css实现一个dropdown
tags:
  - null
categories:
  - Css
date: 2017-02-19 19:49:28
---
当hover上去时出现dropdown：

![](http://7xs8pt.com1.z0.glb.clouddn.com/css%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AAdropdown1.png)

DOM结构：
![](http://7xs8pt.com1.z0.glb.clouddn.com/css%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AAdropdown2.png)

实现原理：

首先，dom结构是统一的，即一个触发源btn，在该btn下是一个span和一个ul，span显示btn上的文字和下拉图标，ul是下拉菜单。注意不可以将ul放在和btn平级的一个div下控制display。这样会出现hover出现ul时再想移到ul上的瞬间ul消失。

然后，css控制btn为relative布局。ul为absolute布局，right为0,display默认为none。
btn在hover时，更改ul的display为block.

附：

    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    border: 1px solid #CCC;
---

发现：firefox里，button里的ul元素无法被选择？
