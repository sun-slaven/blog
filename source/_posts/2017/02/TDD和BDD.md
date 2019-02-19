---
title: TDD和BDD
tags:
  - TDD
  - BDD
categories:
  - 前端测试
date: 2017-02-19 17:42:33
---
**TDD**: Test-driven Development 行为驱动开发，来源于Agile敏捷开发的一个极限编程思想。TDD更偏重与测试代码的功能是否实现正确，它的接口是suite

**BDD**:  Behaviour-driven Development，行为驱动开发.BDD更关注通过测试，观察到程序的行为是否正确,即验证其正确性，因此它的接口是使用**describe**

![](http://7xs8pt.com1.z0.glb.clouddn.com/TDD%E5%92%8CBDD.png)

TDD的接口是比较难用的，大多数时候还是使用的BDD。

我们在写测试用例时，一个被广泛接受的结构是：

1. Setup: 准备好环境和数据，跑这个测试用例之前的准备

2. Execution：执行测试（测试用例的实现的主要代码）

3. Validation：验证结果

4. Cleanup：现场恢复，一般与a相反。不影响跑后面的测试用例
