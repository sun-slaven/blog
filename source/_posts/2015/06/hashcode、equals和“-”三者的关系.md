---
title: 'hash code、equals和“==”三者的关系'
tags:
-
categories:
- java
date: 2015-06-20 22:03:44
updated: 2016-03-25
---

转载于[点击打开链接](http://blog.sina.com.cn/s/blog_5ea3ea4a0100butt.html)，仅供本人收藏使用


两个对象相同(x.equals(y) == true)，则一定有相同的hash code。

**这是java语言的定义：**

因为：Hash，一般翻译做“散列”，也有直接音译为"哈希"的，就是把任意长度的输入（又叫做预映射， pre-image），通过散列算法，变换成固定长度的输出，该输出就是散列&#20540;。这种转换是一种压缩映射，也就是，散列值的空间通常远小于输入的空间，不同的输入可能会散列成相同的输出，而不可能从散列&值来唯一的确定输入值。

<!-- more -->

```
1. 对象相等则hashCode一定相等；
2. hashCode相等对象未必相等。
```

== 是比较**地址**是否相等，JAVA中声明变量都是引用嘛，不同的引用，可能指向同一个地址。

equals 是比较对象的值是否相等。就是判断是否为同一个对象.
***

### equals和==
1. 如果是基本变量，没有hashcode和equals方法，基本变量的比较方式就只有==;

2. 如果是变量，由于在java中所有变量定义都是一个指向实际存储的一个句柄（你可以理解为c++中的指针），在这里==是比较句柄的地址（你可以理解为指针的存储地址），而不是句柄指向的实际内存中的内容，如果要比较实际内存中的内容，那就要用equals方法，但是！！！

3. 如果是你自己定义的一个类，比较自定义类用equals和= =是一样的，都是比较句柄地址，因为自定义的类是继承于object，而object中的equals就是用==来实现的

那为什么我们用的String等等类型equals是比较实际内容呢，是因为String等常用类已经重写了object中的equals方法，让equals来比较实际内容.

### hashcode

在一般的应用中你不需要了解hashcode的用法，但当你用到hashmap，hashset等集合类时要注意下hashcode。

你想通过一个object的key来拿hashmap的value，hashmap的工作方法是，通过你传入的object的hashcode在内存中找地址，当找到这个地址后再通过equals方法来比较这个地址中的内容是否和你原来放进去的一样，一样就取出value。

所以这里要匹配两部分: hashcode和equals

但假如说你new一个object作为key去拿value是永远得不到结果的，因为每次new一个object，这个object的hashcode是永远不同的，所以我们要重写hashcode，你可以令你的hashcode是object中的一个恒量，这样永远可以通过你的object的hashcode来找到key的地址，然后你要重写你的equals方法，使内存中的内容也相等。。。


首先,从语法角度，也就是从强制性的角度来说，hashCode和equals是两个独立的，互不隶属，互不依赖的方法，equals成立与hashCode相等这两个命题之间，谁也不是谁的充分条件或者必要条件。
但是，从为了让我们的程序正常运行的角度，我们应当向Effective Java中所言
重载equals的时候，一定要（正确）重载hashCode ,使得equals成立的时候，hashCode相等，也就是a.equals(b)-> a.hashCode() &nbsp;<wbr>&nbsp;== &nbsp;<wbr>&nbsp;b.hashCode()，或者说此时，equals是hashCode相等的充分条件，hashCode相等是equals的必要条件（从数学课上我们知道它的逆否命题：hashCode不相等也不会equals），但是它的逆命题，hashCode相等一定equals以及否命题不equals时hashCode不等都不成立.


所以，如果面试的时候，最好把hashCode与equals之间没有强制关系，以及根据（没有语法约束力的）规范的角度，应当做到...这两层意思都说出来.

### 总结
equals（）是对象相等性比较，hashCode（）是计算对象的散列&#20540;，当然他们的依据是对象的属性。

对于equals，一般我们认为两个对象同类型并且所有属性相等的时候才是相等的，在类中必须改写equals，因为Object类中的equals只是判断两个引用变量是否引用同一对象，如果不是引用同一对象，即使两个对象的内容完全相同，也会返回false。当然，在类中改写这个equals时，你也可以只对部分属性进行比较，只要这些属性相同就认为对象是相等的。

对于hashCode，只要是用在和哈希运算有关的地方，前面很多兄弟都提到了，和equals一样，在你的类中也应该改写。当然如果两个对象是完全相同的，那么他们的hashCode当然也是一样的，但是象前面所述，规则可以由你自己来定义，因此两者之间并没有什么必然的联系。

当然，大多数情况下我们还是根据所有的属性来计算hashCode和进行相等性比较
