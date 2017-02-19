---
title: 'java的动态绑定与静态绑定'
tags:
-
categories:
- java
date: 2015-06-20 19:50:13
---

注：转载自[点击打开链接](http://blog.sina.com.cn/s/blog_600046120100wdza.html)，仅作个人收藏。

```
Parent p = new Children();
```

这句代码不是很理解，google的过程中引出向上转型 , 要理解向上转型又引出了动态绑定 , 从动态绑定又引出了静态绑定

##### 程序绑定的概念：

绑定指的是一个方法的调用与方法所在的类(方法主体)关联起来。对java来说，绑定分为静态绑定和动态绑定；或者叫做前期绑定和后期绑定
<!-- more -->
1. 静态绑定：
在程序执行前方法已经被绑定，此时由编译器或其它连接程序实现。例如：C。
针对java简单的可以理解为程序编译期的绑定；这里特别说明一点，java当中的方法只有final，static，private和构造方法是前期绑定


2. 动态绑定：
后期绑定：在运行时根据具体对象的类型进行绑定。

若一种语言实现了后期绑定，同时必须提供一些机制，可在运行期间判断对象的类型，并分别调用适当的方法。也就是说，编译器此时依然不知道对象的类型，但方法调用机制能自己去调查，找到正确的方法主体。不同的语言对后期绑定的实现方法是有所区别的。但我们至少可以这样认为：它们都要在对象中安插某些特殊类型的信息。

##### 动态绑定的过程：
1.	虚拟机提取对象的实际类型的方法表；
2.	虚拟机搜索方法签名；
3.	调用方法。

##### 关于绑定相关的总结：
在了解了三者的概念之后，很明显我们发现java属于后期绑定。在java中，几乎所有的方法都是后期绑定的，在运行时动态绑定方法属于子类还是基类。但是也有特殊，针对static方法和final方法由于不能被继承，因此在编译时就可以确定他们的&#20540;，他们是属于前期绑定的。特别说明的一点是，private声明的方法和成员变量不能被子类继承，所有的private方法都被隐式的指定为final的(由此我们也可以知道：将方法声明为final类型的一是为了防止方法被覆盖，二是为了有效的关闭java中的动态绑定)。java中的后期绑定是有JVM来实现的，我们不用去显式的声明它，而C&#43;&#43;则不同,必须明确的声明某个方法具备后期绑定。

java当中的向上转型或者说多态是借助于动态绑定实现的，所以理解了动态绑定，也就搞定了向上转型和多态。

前面已经说了对于java当中的方法而言，除了final，static，private和构造方法是前期绑定外，其他的方法全部为动态绑定。而动态绑定的典型发生在父类和子类的转换声明之下：

比如：Parent p = new Children();

其具体过程细节如下：

1. 编译器检查对象的声明类型和方法名。假设我们调用x.f(args)方法，并且x已经被声明为C类的对象，那么编译器会列举出C类中所有的名称为f的方法和从C类的超类继承过来的f方法

2. 接下来编译器检查方法调用中提供的参数类型。如果在所有名称为f 的方法中有一个参数类型和调用提供的参数类型最为匹配，那么就调用这个方法，这个过程叫做“重载解析”&nbsp;<wbr>

3. 当程序运行并且使用动态绑定调用方法时，虚拟机必须调用同x所指向的对象的实际类型相匹配的方法版本。假设实际类型为D(C的子类)，如果D类定义了f(String)那么该方法被调用，否则就在D的超类中搜寻方法f(String),依次类推

&nbsp;<wbr>

上面是理论，下面看几个示例（示例来自网络）：

```
public class Father {
　　public void method() {
　　　 System.out.println("父类方法，对象类型：" + this.getClass());
　　}
}
```
```
public class Son extends Father {
　　public static void main(String[] args) {
　　　 Father sample = new Son();//向上转型
　　　 sample.method();
　　}
}
```
声明的是父类的引用，但是执行的过程中调用的是子类的对象，程序首先寻找子类对象的method方法，但是没有找到，于是向上转型去父类寻找
```
public class Son extends Father {

　　public void method() {
　　　 System.out.println("子类方法，对象类型:" + this.getClass());
　　}

　　public static void main(String[] args) {
　　　 Father sample = new Son();//向上转型
　　　 sample.method();
　　}
}

```
由于子类重写了父类的method方法，根据上面的理论知道会去调用子类的method方法去执行，因为子类对象有method方法而没有向上转型去寻找


前面的理论当中已经提到了java的绑定规则，由此可知，在处理java类中的成员变量时，并不是采用运行时绑定，而是一般意义上的静态绑定。所以在向上转型的情况下，对象的方法可以找到子类，而对象的属性还是父类的属性。
```
public class Father {
　　protected String name="父亲属性";
　　public void method() {
　　　 System.out.println("父类方法，对象类型：" +  this.getClass());
　　}
}
```
```
public class Son extends Father {
　　protected String name="儿子属性";
　　public void method() {
　　　 System.out.println("子类方法，对象类型" +  this.getClass());
　　}
　　public static void main(String[] args) {
　　　 Father sample = new Son();//向上转型
　　　 System.out.println("调用的成员：" + sample.name);
　　}
}
```
结论，调用的成员为父亲的属性。

这个结果表明，子类的对象(由父类的引用handle)调用到的是父类的成员变量。所以必须明确，运行时（动态）绑定针对的范畴只是对象的方法。

现在试图调用子类的成员变量name，该怎么做？最简单的办法是将该成员变量封装成方法getter形式。

```
public class Father {
　　protected String name = "父亲属性";
　　public String getName() {
　　　 return name;
　　}
　　public void method() {
　　　 System.out.println("父类方法，对象类型：" + this.getClass());
　　}
}
```
```
public class Son extends Father {
　　protected String name="儿子属性";
　　public String getName() {
　　　 return name;
　　}
　　public void method() {
　　　 System.out.println("子类方法，对象类型：" +  this.getClass());
　　}
　　public static void main(String[] args) {
　　　 Father sample = new Son();//向上转型
　　　 System.out.println("调用的成员：" + sample.getName());
　　}
}
```
结果：调用的是儿子的属性
