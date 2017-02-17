---
title: 'js对象类型之prototype属性的探索'
date: 2015-09-26 18:03:53
updated: 2016-03-23 13:51:50
tags:
- prototype
catagories:
- Javascript基础知识
---

<span style="color:#ff0000">本篇尚未写完，初步排版</span>

作为所有的对象都具有的属性之一，它叫做原型。初始指向一个叫做Prototype的对象（它一开始什么都没有）
<!-- more -->
作用主要是实现类&#20284;“继承”的形式、创建多个对象的实例方便。

&nbsp;

对象的prototype属性指向一个对应的Prototype对象，初始&#20540;为undefined

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; var a = new Object();

&nbsp; &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;alert(a.prototype);//undefined

&nbsp;

该属性被赋予一些属性或者方法的时候，这些属性和方法实际是加到了Prototype对象中作为Prototype对象的属性和方法，

&nbsp;

该属性被赋予一个对象时，那就不同了，此时的prototype克隆了该对象所有的属性和方法，可以把prototype看做是一个“小容器”，所以具有prototype属性的该对象继承了被克隆对象。如果被克隆对象的prototype属性指向另一个被克隆对象时，此时就成了原型链，它的作用就相当于继承的概念，当调用方法的时候，如果对象本身没有找到，就会上溯这个原型链直到被找到或者到达顶端Object对象的prototype属性的null&#20540;。

&nbsp;

如果先被赋&#20540;一些属性和方法然后被赋&#20540;一个对象，那么该对象就会覆盖之前赋&#20540;的所有内容，因为Prototype对象

&nbsp;

&nbsp;

普通对象和Function对象对于Prototype好像不同

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; vara = new Object();

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; console.log(a.prototype);//undefined

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; vara = new String();

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; console.log(a.prototype);//undefined

&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; vara = new Array();

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; console.log(a.prototype);//undefined

&nbsp;

&nbsp;

******************************************************************

varb = new Function();

console.log(b.prototype);// Object { , 等 1 项… }

console.log( typeof b.prototype ); //object

console.log( b.prototype instanceof(Object));//true

console.log( b.prototypeinstanceof(Function) );//false

说明：<span style="color:red">Function</span><span style="color:red">对象的</span><span style="color:red">prototype</span><span style="color:red">属性为</span><span style="color:red">Object</span><span style="color:red">对象，而不是</span><span style="color:red">Function</span><span style="color:red">对象。</span>

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; var b = new Function();

&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;b.prototype.myname= &quot;myname&quot;;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b.prototype.func=function(){alert(&quot;我是func方法&quot;)};

&nbsp;

&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;console.log(b.prototype);// Object { name:&quot;myname&quot;, func: a.prototype.func(), 等 1 项… }

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;console.log(typeof b.prototype);//object

&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;console.log(b.prototypeinstanceof(Object))//true

&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; alert(b.prototype.myname)//myname

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;b.prototype.func();//我是func方法&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

<span style="color:red">说明：</span><span style="color:red">name</span><span style="color:red">属性和</span><span style="color:red">func</span><span style="color:red">方法都被加到</span><span style="color:red">prototype</span><span style="color:red">属性指向的</span><span style="color:red">Object</span><span style="color:red">对象中去了。</span>

<span style="color:red">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>var b = new Function();

<span style="color:#0D0D0D">&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;b.prototype.myname= &quot;myname&quot;;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp; b.prototype.func=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">func</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">b.prototype=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">func</span><span style="color:#0D0D0D">对象</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">b.prototype.myname1=&quot;myname1&quot;;</span>

<span style="color:#0D0D0D">b.prototype.func1=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">func</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">1&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; console.log(b.prototype);//functionb.prototype()</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; console.log(typeof b.prototype);//function</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; console.log(b.prototypeinstanceof(Object));//true</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; console.log(b.prototypeinstanceof(Function));//true</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>alert(b.prototype.myname);//undefined

b.prototype.func();//TypeError:b.prototype.func is not a function

console.log(b.prototype.myname1);//myname1

b.prototype.func1()//<span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">func</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">1</span>

b.prototype()//<span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">func</span><span style="color:#0D0D0D">对象</span><span style="color:#0D0D0D">à</span><span style="color:#0D0D0D">把</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象看做一般方法使用</span>

<span style="color:red">说明：当给</span><span style="color:red">prototype</span><span style="color:red">赋&#20540;一个新对象的时候，那么</span><span style="color:red">prototype</span><span style="color:red">属性指向的对象就不是</span><span style="color:red">Object</span><span style="color:red">而是新对象了，之前赋给</span><span style="color:red">Object</span><span style="color:red">的所有的属性和方法全部丢失！同样可以添加方法和属性到这个新对象。</span>

<span style="color:red">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp; </span><span style="color:#0D0D0D">var b =new Function();</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.newname=&quot;newname&quot;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.newfunc=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">newfunc</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.prototype=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">func</span><span style="color:#0D0D0D">对象</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.prototype.newname=&quot;pnewname&quot;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.prototype.newfunc=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">pnewfunc</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>

<span style="color:#0D0D0D">&nbsp; alert(b.newname)//newname</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.newfunc()//</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">newfunc</span><span style="color:#0D0D0D">方法</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; alert(b.prototype.newname);//pnewname</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.prototype.newfunc();//</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">pnewfunc</span><span style="color:#0D0D0D">方法</span>

<span style="color:red">说明：</span><span style="color:red">b</span><span style="color:red">对象的内容和</span><span style="color:red">b</span><span style="color:red">的</span><span style="color:red">prototype</span><span style="color:red">属性储存的内容没有任何关系！属性和方法一样也不会覆盖。</span><span style="color:red">b.prototype</span><span style="color:red">储存的</span><span style="color:red">Function</span><span style="color:red">对象的属性和方法不属于</span><span style="color:red">b</span><span style="color:red">对象，</span><span style="color:red">
 b</span><span style="color:red">对象不可以直接使用</span><span style="color:red">b.prototype</span><span style="color:red">属性储存的对象中的属性和方法</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; var b = newFunction();</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;b.newname=&quot;bnewname&quot;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;b.newfunc=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">bnewfunc</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;b.prototype=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">b</span><span style="color:#0D0D0D">的储存对象</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;b.prototype.newname=&quot;pbnewname&quot;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; b.prototype.newfunc=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">pbnewfunc</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; var c = newFunction();</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;c.newname=&quot;cnewname&quot;</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;c.newfunc=function(){alert(&quot;</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">cnewfunc</span><span style="color:#0D0D0D">方法</span><span style="color:#0D0D0D">&quot;)};</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; c.prototype=b;//</span><span style="color:red">注意这里不是</span><span style="color:red">b()</span><span style="color:red">，因为</span><span style="color:red">b</span><span style="color:red">已经是对象了。写</span><span style="color:red">b()</span><span style="color:red">就会使其变为第一个</span><span style="color:red">Function</span><span style="color:red">对象</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; </span>

<span style="color:#0D0D0D">&nbsp;&nbsp;alert(c.newname)//cnewname</span>

<span style="color:#0D0D0D">&nbsp;&nbsp; c.newfunc()//</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">cnewfunc</span><span style="color:#0D0D0D">方法</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;alert(c.prototype.newname);//bnewname</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;c.prototype.newfunc();//</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">bnewfunc</span><span style="color:#0D0D0D">方法</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;alert(c.prototype.prototype.newname)//pbnewname</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;c.prototype.prototype.newfunc()//</span><span style="color:#0D0D0D">我是</span><span style="color:#0D0D0D">pbnewfunc</span><span style="color:#0D0D0D">方法</span>

<span style="color:red">&nbsp;</span>

<span style="color:red">说明：以上代码探究了“继承的情况”，发现，</span><span style="color:red">c</span><span style="color:red">对象可以正常调用</span><span style="color:red">prototype</span><span style="color:red">属性储存的</span><span style="color:red">b</span><span style="color:red">克隆对象的属性和方法，更是可以调用</span><span style="color:red">prototype</span><span style="color:red">属性储存的</span><span style="color:red">b</span><span style="color:red">克隆对象的</span><span style="color:red">prototype</span><span style="color:red">属性储存的</span><span style="color:red">Function</span><span style="color:red">克隆对象的属性和方法，即便这三者都重名，也没有发生所谓的覆盖或者“重写”现象，所以本质上和</span><span style="color:red">java</span><span style="color:red">的继承完全不同。</span>

<span style="color:red">&nbsp;</span>

<span style="color:red; background:#D9D9D9">探究原型链：</span>

<span style="color:#0D0D0D">var uw3c=newFunction()//</span><span style="color:#0D0D0D">创建</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp; uw3c.prototype.prop = &quot;b&quot;;</span>

<span style="color:#0D0D0D">&nbsp; var test = new uw3c();//</span><span style="color:#0D0D0D">创建</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象</span><span style="color:#0D0D0D">uw3c</span><span style="color:#0D0D0D">的一个实例</span>

<span style="color:#0D0D0D">&nbsp; console.log(uw3c.prop);//undefined</span>

<span style="color:#0D0D0D">&nbsp; console.log(test.prop);//b</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; console.log(test.prototype);//undefined&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>

<span style="color:#0D0D0D">结论：对象拥有</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性，对象本身却不可以直接访问该属性里的内容，对象的实例是</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">对象，和对象类型没有关系，也就是丢失了对象的所有的内容，对象的实例没有</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性，但是对象的实例直接拥有了对象的</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性里的内容。查阅资料从而知道：</span><span style="color:red">test.__proto__
 =uw3c.prototype</span><span style="color:#0D0D0D">，</span><span style="color:#0D0D0D">test</span><span style="color:#0D0D0D">对象的</span><span style="color:#0D0D0D">__proto__</span><span style="color:#0D0D0D">属性内的内容可以被</span><span style="color:#0D0D0D">test</span><span style="color:#0D0D0D">对象直接访问。</span>

<span style="color:#0D0D0D">&nbsp; var uw3c=newFunction()</span>

<span style="color:#0D0D0D">&nbsp; var test = newuw3c();</span>

<span style="color:#0D0D0D">&nbsp; var test2 = newuw3c();</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp; console.log(test)</span>

<span style="color:#0D0D0D">&nbsp;console.log(test.__proto__ == uw3c.prototype)//true</span>

<span style="color:#0D0D0D">&nbsp;console.log(test2.__proto__ == uw3c.prototype)//true</span>

<span style="color:#0D0D0D">&nbsp;console.log(uw3c.__proto__ == Function.prototype)//true</span>

<span style="color:#0D0D0D">&nbsp;console.log(Function.__proto__ == Function.prototype)//true</span>

<span style="color:#0D0D0D">&nbsp;console.log(Function.prototype)//function(){}</span>

<span style="color:#0D0D0D">结论：</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象的多个实例互不干扰。</span>

<span style="color:#0D0D0D">test.__proto__ ==uw3c.prototype</span>

<span style="color:#0D0D0D">uw3c.__proto__ ==Function.prototype</span>

<span style="color:#0D0D0D">Function.__proto__== Function.prototype</span>

<span style="color:#0D0D0D">Function.prototype</span><span style="color:#0D0D0D">为：</span><span style="color:#0D0D0D">function(){}</span>

<span style="color:red">这就是原型链：实例的</span><span style="color:red">__proto__</span><span style="color:red">指向对象的</span><span style="color:red">prototype,</span><span style="color:red">对象的</span><span style="color:red">__proto__</span><span style="color:red">指向其对应的内置对象的</span><span style="color:red">prototype</span><span style="color:red">，所有的内置对象（</span><span style="color:red">Object</span><span style="color:red">、</span><span style="color:red">Array</span><span style="color:red">）的</span><span style="color:red">__proto__</span><span style="color:red">指向</span><span style="color:red">Function</span><span style="color:red">对象的</span><span style="color:red">prototype</span><span style="color:red">，它的&#20540;就是</span><span style="color:red">function(){}</span><span style="color:red">。</span>

<span style="color:red">&nbsp;console.log(Object.__proto__)//function(){}</span>

<span style="color:red">&nbsp;console.log(Array.__proto__)//function(){}</span>

<span style="color:red">&nbsp;console.log(String.__proto__)//function(){}</span>

<span style="color:#0D0D0D">可通过</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性指定继承对象，而引擎自动通过</span><span style="color:#0D0D0D">__proto__</span><span style="color:#0D0D0D">属性实现继承效果。</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:red">总结：</span>

<span style="color:#0D0D0D">1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">普通对象（包括</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">对象）的</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性</span><span style="color:red">初始</span><span style="color:#0D0D0D">为</span><span style="color:#0D0D0D">undefined</span><span style="color:#0D0D0D">类型，但是</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象则为</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">对象。并不存在所谓的</span><span style="color:#0D0D0D">Prototype</span><span style="color:#0D0D0D">对象！</span>

<span style="color:#0D0D0D">2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">1)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">针对于一般对象，若是直接赋&#20540;属性或者方法，则会报错，因为</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性默认为</span><span style="color:#0D0D0D">undefined</span><span style="color:#0D0D0D">类型，并非一个对象，自然不可以添加属性和方法。</span>

<span style="color:#0D0D0D">2)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">针对于</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象：</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性相当于一个独立的空间、默认存放</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">克隆对象。若是直接赋&#20540;属性或者方法，这些属性或者方法则加到了默认的</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">对象中。</span>

<span style="color:#0D0D0D">3)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">针对于所有对象：若是直接赋&#20540;一个对象，则</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性这个空间储存该对象的克隆，</span><span style="color:#0D0D0D">undefined</span><span style="color:#0D0D0D">和默认的</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">对象被丢弃。可以对该克隆对象添加属性和方法。拥有</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性的对象作为大空间，并不意味着可以直接调用</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性空间内储存的克隆对象的属性和方法，必须通过</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性找到克隆对象，然后由克隆对象调用。大空间里的属性和方法与</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性空间里的属性和方法</span><span style="color:red">没任何关系，同名也无所谓，不会产生覆盖</span><span style="color:#0D0D0D">。</span>

<span style="color:#0D0D0D">3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">通过</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性达到“继承”效果，就是给</span><span style="color:#0D0D0D">C</span><span style="color:#0D0D0D">对象的</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性赋&#20540;</span><span style="color:#0D0D0D">B</span><span style="color:#0D0D0D">对象，</span><span style="color:#0D0D0D">B</span><span style="color:#0D0D0D">对象的</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性赋&#20540;</span><span style="color:#0D0D0D">A</span><span style="color:#0D0D0D">对象，在效果上形成了继承，即</span><span style="color:#0D0D0D">B</span><span style="color:#0D0D0D">对象可以“拥有”</span><span style="color:#0D0D0D">A</span><span style="color:#0D0D0D">克隆对象的内容，</span><span style="color:#0D0D0D">C</span><span style="color:#0D0D0D">对象可以“拥有”</span><span style="color:#0D0D0D">B</span><span style="color:#0D0D0D">克隆对象的内容，也“拥有”了</span><span style="color:#0D0D0D">A</span><span style="color:#0D0D0D">克隆对象内容。</span>

<span style="color:red">但是需要注意的是</span><span style="color:#0D0D0D">：根据结论</span><span style="color:#0D0D0D">2</span><span style="color:#0D0D0D">，</span><span style="color:#0D0D0D">C</span><span style="color:#0D0D0D">对象的属性和方法和</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性空间储存的</span><span style="color:#0D0D0D">B</span><span style="color:#0D0D0D">克隆对象的属性和方法毫不相干，</span><span style="color:#0D0D0D">B</span><span style="color:#0D0D0D">对象的属性和方法和</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性空间储存的</span><span style="color:#0D0D0D">A</span><span style="color:#0D0D0D">克隆对象的属性和方法毫不相干，</span><span style="color:#0D0D0D">也就是说，不会产生类&#20284;</span><span style="color:#0D0D0D">java</span><span style="color:#0D0D0D">中继承的重写效果。即便三个对象拥有同名的属性和方法，也不会相互覆盖掉！</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">因为结论</span><span style="color:#0D0D0D">3</span><span style="color:#0D0D0D">的“继承”效果，产生了原型链。</span>

<span style="color:#0D0D0D">varuw3c=new Function()//</span><span style="color:#0D0D0D">创建</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象</span>

<span style="color:#0D0D0D">&nbsp;</span>

<span style="color:#0D0D0D">&nbsp; uw3c.prototype.prop = &quot;b&quot;;</span>

<span style="color:#0D0D0D">&nbsp; var test = new uw3c();//</span><span style="color:#0D0D0D">创建</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象</span><span style="color:#0D0D0D">uw3c</span><span style="color:#0D0D0D">的一个实例</span>

<span style="color:#0D0D0D">&nbsp; console.log(uw3c.prop);//undefined</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;console.log(test.prop);//b</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; console.log(test.prototype);//undefined&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>

<span style="color:#0D0D0D">结论：对象拥有</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性，对象本身却不可以直接访问该属性里的内容，对象的实例是</span><span style="color:#0D0D0D">Object</span><span style="color:#0D0D0D">对象，和对象类型没有关系，也就是丢失了对象的所有的内容（除了</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性储存的内容），对象的实例没有</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性，但是对象的实例直接拥有了对象的</span><span style="color:#0D0D0D">prototype</span><span style="color:#0D0D0D">属性里的内容。查阅资料从而知道：</span><span style="color:red">test.__proto__
 =uw3c.prototype</span>

<span style="color:red">Function</span><span style="color:red">对象的实例</span><span style="color:red">.__proto__== Function</span><span style="color:red">对象</span><span style="color:red">.prototype==Object</span><span style="color:red">对象</span><span style="color:red">(</span><span style="color:red">默认。可被指定修改</span><span style="color:red">)</span>

<span style="color:red">Function</span><span style="color:red">对象</span><span style="color:red">.__proto__==Function</span><span style="color:red">内置对象</span><span style="color:red">.prototype== Function</span><span style="color:red">内置对象</span><span style="color:red">.__proto__==</span><span style="color:red">
 Object</span><span style="color:red">对象</span>

<span style="color:#0D0D0D">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>

<span style="color:red">Object</span><span style="color:red">对象</span><span style="color:red">.__proto__==Object</span><span style="color:red">对象</span><span style="color:red">.prototype</span><span style="color:red">（作为</span><span style="color:red">Function</span><span style="color:red">对象）</span><span style="color:red">==</span><span style="color:red">特殊的</span><span style="color:red">Object</span><span style="color:red">对象（它的</span><span style="color:red">__proto__==null</span><span style="color:red">）</span>

<span style="color:red">Object</span><span style="color:red">内置对象</span><span style="color:red">.prototype==</span><span style="color:red">特殊的</span><span style="color:red">Object</span><span style="color:red">对象（它的</span><span style="color:red">__proto__==null</span><span style="color:red">）</span>

<span style="color:red">Object</span><span style="color:red">内置对象</span><span style="color:red">.__proto__==??.prototype==Object</span><span style="color:red">对象</span>

<span style="color:red">其他对象</span><span style="color:red">.__proto__==Function</span><span style="color:red">对象</span><span style="color:red">.__proto__==Function</span><span style="color:red">内置对象</span><span style="color:red">.prototype== Function</span><span style="color:red">内置对象</span><span style="color:red">.__proto__==
 Object</span><span style="color:red">对象</span>

<span style="color:red">其他内置对象</span><span style="color:red">.</span>

<span style="color:#0D0D0D">一个对象的</span><span style="color:#0D0D0D">__proto__</span><span style="color:#0D0D0D">属性的内容可以被对象直接访问！</span>

<span style="color:#0D0D0D">![]()

</span>

<span style="color:#0D0D0D">注：图片来源于网络，自己花了半天发现还是画错了，最后决定用这张图</span>

            <div>
                作者：z893196569 发表于2015/9/26 18:03:53 [原文链接](http://blog.csdn.net/z893196569/article/details/48752877)
            </div>
            <div>
            阅读：60 评论：0 [查看评论](http://blog.csdn.net/z893196569/article/details/48752877#comments)
            </div>
