---
title: 'js对象类型之本地对象'
tags:
- js本地对象
categories:
- Javascript
date: 2015-09-26 16:08:14
---

## <span style="font-weight:normal"><span style="color:#ff0000">本篇博客为初稿，稍微整理了一下，有些地方说的不准确。仅作为个人学习心得记录使用。</span></span>

## 本地对象相对于宿主对象而言，都是属于object数据类型的范畴。

> <div><span style="background-color:rgb(51,204,0)">以下讲解的所有的对象都是本地对象，而本地对象又分为内置对象和自定义对象，除去Global对象和Math对象肯定为内置对象外，其他所有的对象在直接使用字面的情况下作为内置对象，在使用new构造、普通函数名构造或者字面量形式构造的对象都是自定义对象。自定义对象不可以使用内置对象中全大写的属性（相当于java中类的常量的概念）</span></div>
<!-- more -->
## 一、Global对象

> 全局对象是特殊的内置对象。无法使用new关键字创建实例
>
> 所有的全局方法都集中在这个对象中。包含isNaN（）、parseInt（）、String（）等方法
>
> 除了本身具有的<span style="color:red">undefined</span>、NaN等属性外，<span style="color:#ff0000">在顶层 JavaScript 代码中声明的所有变量都将成为全局对象的属性。</span>
>
> 它具有的详细的方法和属性参考：[http://www.w3school.com.cn/jsref/jsref_obj_global.asp](http://www.w3school.com.cn/jsref/jsref_obj_global.asp)。

## 二、&nbsp;Math对象

> 和Global对象一样，作为特殊的内置对象，不使用new关键字。
>
> Math 对象用于执行数学任务。
>
> var pi_value=Math.PI;
>
> var sqrt_value=Math.sqrt(15);
>
> 它具有的详细的方法和属性参考：[http://www.w3school.com.cn/jsref/jsref_obj_math.asp](http://www.w3school.com.cn/jsref/jsref_obj_math.asp)。

## 三、&nbsp;String对象

### 1.创建 String 对象的语法：

> <span style="color:red">构造方法创建形式：</span><span style="color:red">new String(s);</span>
>
> <span style="color:red">全局方法创建形式：</span><span style="color:red">String(s);&nbsp;&nbsp;&nbsp; </span>
>
> <span style="color:red">（全局方法，是</span><span style="color:red">Global</span><span style="color:red">对象的方法）</span>
>
> <span style="color:red">字面量定义形式：</span><span style="color:red">var x = “xx”</span><span style="color:red">（下面都提到）</span>
> 说明：
>
> a)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当 String() 和运算符 new 一起作为构造函数使用时，它返回一个新创建的 String 对象，存放的是字符串 s 或 s 的字符串表示。
>
> b)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当不用 new 运算符调用 String() 时，它只把 s 转换成原始的字符串，并返回转换后的&#20540;。
>
> c)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;字面量形式<span style="color:red">本质上没有创建对象</span>，但是编译器会将其当做对象处理，该对象xx的引用x具有String对象的一切性质

### 2.对象的属性

> &nbsp;属性 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> constructor&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 对创建该对象的函数的引用
>
> length &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 字符串的长度
>
> prototype 允许您向对象添加属性和方法

### 3.对象的方法

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 参考：[http://www.w3school.com.cn/jsref/jsref_obj_string.asp](http://www.w3school.com.cn/jsref/jsref_obj_string.asp)。

## 四、&nbsp;Number对象

### 1.创建对象的语法：

> <span style="color:#cc0000">var myNum=new Number(value);</span>
>
> <span style="color:#cc0000">var myNum=Number(value); （全局方法，是Global对象的方法）</span>
>
> <span style="color:#cc0000">字面量形式：var myNum = 1；</span>
> 说明：当 Number() 和运算符 new 一起作为构造函数使用时，它返回一个新创建的 Number 对象。如果不用 new 运算符，把 Number() 作为一个函数来调用，它将把自己的参数转换成一个原始的数&#20540;，并且返回这个&#20540;（如果转换失败，则返回 NaN）。

### 2.对象的属性

> constructor &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 对创建该对象的函数的引用
>
> prototype &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 允许您向对象添加属性和方法
> > <span style="color:#ff0000">注：其中大写的属性比较特殊，类&#20284;于java中的常量，并不属于对象的实例，也并不能通过对象的实例调用，而是应该通过对象直接访问。</span>
> <span style="color:#ff0000">&nbsp;<span style="white-space:pre"> </span>比如这样使用属性 MAX_VALUE 是正确的：</span>
> > > <span style="color:#ff0000">var big = Number.MAX_VALUE</span>
>
> > > <span style="color:#ff0000">但是这样是错误的：</span>
>
> > > <span style="color:#ff0000">var n= new Number(2);</span>
>
> > > <span style="color:#ff0000">var big = n.MAX_VALUE</span>

### 3.对象的方法

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; valueOf &nbsp;&nbsp;&nbsp; 返回一个 Number 对象的基本数字&#20540;。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; toString &nbsp;&nbsp;&nbsp; 把数字转换为字符串，使用指定的基数。

> 更多方法和属性参考：[http://www.w3school.com.cn/jsref/jsref_obj_number.asp](http://www.w3school.com.cn/jsref/jsref_obj_number.asp)。

## 五、&nbsp;Boolean对象

### 1.创建的语法：

> <span style="color:#ff0000">new Boolean(value);&nbsp;&nbsp;&nbsp;&nbsp; //构造函数</span>
>
> <span style="color:#ff0000">Boolean(value);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //转换函数</span>
>
> <span style="color:#ff0000">字面量形式：var x = true；</span>
> 注：如果省略 value 参数，或者设置为 0、-0、null、&quot;&quot;、false、undefined 或 NaN，则该对象设置为 false。否则设置为 true（即使 value 参数是字符串 &quot;false&quot;）。

### 2.对象属性

> 属性 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> constructor &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回对创建此对象的 Boolean 函数的引用
>
> prototype &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 使您有能力向对象添加属性和方法。

### &nbsp;3.对象方法

> 方法 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> toSource() &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回该对象的源代码。
>
> toString() &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 把逻辑&#20540;转换为字符串，并返回结果。
>
> valueOf() &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回 Boolean 对象的原始&#20540;。

## 六、&nbsp;Array对象

### 1.创建对象的语法：

> new Array();
>
> new Array(size);
>
> new Array(element0, element1, ..., elementn);
>
> &nbsp;
> 字面量形式：var x =[1,2]；

### &nbsp;2\. Array对象属性

> 属性 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> constructor &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回对创建此对象的数组函数的引用。
>
> length &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 设置或返回数组中元素的数目。
>
> prototype 使您有能力向对象添加属性和方法。

3\. Array 对象方法

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; push()&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 向数组的末尾添加一个或更多元素，并返回新的长度。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; reverse()&nbsp; 颠倒数组中元素的顺序。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; toString() 把数组转换为字符串，并返回结果。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; valueOf() 返回数组对象的原始&#20540;

更多方法参考[http://www.w3school.com.cn/jsref/jsref_obj_array.asp](http://www.w3school.com.cn/jsref/jsref_obj_array.asp)。

## 七、&nbsp;Date对象

### 1\. 创建 Date 对象的语法：

> var myDate=new Date()
>
> Date 对象会自动把当前日期和时间保存为其初始&#20540;。

### 2\. Date 对象属性

> 属性 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> constructor &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回对创建此对象的 Date 函数的引用。
>
> prototype 使您有能力向对象添加属性和方法

### 3\. Date 对象方法

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;方法非常多，参考：[http://www.w3school.com.cn/jsref/jsref_obj_date.asp](http://www.w3school.com.cn/jsref/jsref_obj_date.asp)。

## 八、&nbsp;RegExp对象

RegExp 对象表示正则表达式，它是对字符串执行模式匹配的强大工具。

### 1\. 直接量语法

<span style="white-space:pre"></span>/pattern/attributes

### 2\. 创建 RegExp 对象的语法：

<span style="white-space:pre"></span>new RegExp(pattern, attributes);

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;说明：

&nbsp; &nbsp; &nbsp; &nbsp; 参数

> 参数 pattern 是一个字符串，指定了正则表达式的模式或其他正则表达式。
>
> 参数 attributes 是一个可选的字符串，包含属性 &quot;g&quot;、&quot;i&quot; 和 &quot;m&quot;，分别用于指定全局匹配、区分大小写的匹配和多行匹配。ECMAScript 标准化之前，不支持 m 属性。如果 pattern 是正则表达式，而不是字符串，则必须省略该参数。

<span style="white-space:pre"></span>返回&#20540;

> 一个新的 RegExp 对象，具有指定的模式和标志。如果参数 pattern 是正则表达式而不是字符串，那么 RegExp() 构造函数将用与指定的 RegExp 相同的模式和标志创建一个新的 RegExp 对象。
>
> 如果不用 new 运算符，而将 RegExp() 作为函数调用，那么它的行为与用 new 运算符调用时一样，只是当 pattern 是正则表达式时，它只返回 pattern，而不再创建一个新的 RegExp 对象。

<span style="white-space:pre"></span>抛出

> SyntaxError - 如果 pattern 不是合法的正则表达式，或 attributes 含有 &quot;g&quot;、&quot;i&quot; 和 &quot;m&quot; 之外的字符，抛出该异常。
>
> TypeError - 如果 pattern 是 RegExp 对象，但没有省略 attributes 参数，抛出该异常。

### 3\. 具体使用

### <span style="white-space:pre"></span><span style="font-weight:normal">请详细阅读</span>[http://www.w3school.com.cn/jsref/jsref_obj_regexp.asp](http://www.w3school.com.cn/jsref/jsref_obj_regexp.asp)。

## 八、&nbsp;Function对象

> <span style="color:red">Function</span><span style="color:red">对象即函数，每个函数都是一个</span><span style="color:red">Function</span><span style="color:red">对象实例。</span>
>
> <span style="color:red">因为函数创建方法多样，所以</span><span style="color:red">Function</span><span style="color:red">对象创建也就有多种方式。</span>

### 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;创建对象

> #### 1)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通过Function对象的构造方法或全局方法创建
>
> > new Function( [ argName1 [,argName1 [, argNameN... [, funcBody ]]]] )
>
> > Function( [argName1 [, argName1 [, argNameN... [, funcBody ]]]] )
>
> > 参数
>
> > 参数&nbsp;&nbsp;&nbsp; 描述
>
> > argName1&nbsp;&nbsp;&nbsp; 可选/String类型 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 定义的第1个参数的名称。
>
> > argName2&nbsp;&nbsp;&nbsp; 可选/String类型&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 定义的第2个参数的名称。
>
> > argNameN&nbsp;&nbsp; 可选/String类型&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 定义的第N个参数的名称，可以有任意多个。
>
> > funcBody&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可选/String类型&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 定义的函数主体，即函数内部的执行代码，默认为空字符串(&quot;&quot;)。Function()会把传入的最后一个参数作为函数定义的执行代码，之前的所有参数均依次作为函数定义的参数。
>
> > 代码示例：
>
> > &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
> >
> > <pre name="code" class="javascript">// 定义一个求和函数：带有2个参数x、y。
> > var sum = new Function(&quot;x&quot;, &quot;y&quot;, &quot;return x +y;&quot;);
> > // 定义一个输出函数：没有定义参数，输出&quot;CodePlayer&quot;
> > var foo = Function(&#39;var name=&quot;CodePlayer&quot;;document.writeln(name);&#39;);
> >
> > // 执行函数
> > document.writeln( sum( 12, 23 ) ); // 35
> > foo(); // CodePlayer
> >
> > document.writeln( typeof sum ); // function
> > document.writeln( sum instanceof Function ); // true
> > document.writeln( sum instanceof Object ); //true</pre>
> #### _2)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:red">字面量形式：直接以</span><span style="color:red">function</span><span style="color:red">关键字形式声明函数，一旦申明即创建</span><span style="color:red">Function</span><span style="color:red">对象（就像</span><span style="color:red">string</span><span style="color:red">字符串，可以</span><span style="color:red">new</span><span style="color:red">，也可以直接以字面量形式创建虽然不是对象，但是相当于对象，具有对象的所有性质。）：</span>_
>
> > ##### a)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;声明式：
>
> > &nbsp; &nbsp; &nbsp;
> >
> > <pre name="code" class="javascript">   function funcName(argName1, argName2, argNameN){
> >     // funcBody 这里是函数的执行代码
> > }
> >                                                         代码举例：
> >                                                                       function sum(x, y){
> >     return x + y;  
> > }
> >
> > function foo(){
> >     var name = &quot;CodePlayer&quot;;
> >     document.writeln( name );
> > }
> >
> > // 执行函数
> > document.writeln(sum( 12, 23 ) ); // 35
> > foo(); //CodePlayer    此时的foo就是一个Function对象，使用只需要加（），无需再new foo（）
> >
> > document.writeln(typeof sum ); // function
> > document.writeln(sum instanceof Function ); // true
> > document.writeln(sum instanceof Object ); // true</pre>
>
> > ##### b)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;匿名表达式：
>
> > <pre name="code" class="javascript">var foo =function(){
> >     var name = &quot;CodePlayer&quot;;
> >     document.writeln( name );
> > };
> > foo(); // CodePlayer</pre>
>
> > ##### c)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;匿名自调用：
>
> > <pre name="code" class="javascript">// 在匿名函数的定义代码外面必须加小括号，表示强迫计算并返回计算结果(否则JS只是解析该匿名函数，但无法获得函数引用，进而无法执行该函数)
> > // 定义代码后面加上小括号，里面可以传入执行所需的参数(这里为2和3)
> > ( function(x, y){
> >     document.writeln( x + y );
> > } )(2, 3); // 5
> >
> > // 上述匿名函数立即执行的代码，还可以如下书写(请注意小括号的位置和匹配)：
> > ( function(x, y){
> >     document.writeln( x + y );
> > }(2, 3) ) ; // 5</pre>

### 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象属性

> 属性&nbsp;&nbsp;&nbsp; 描述
>
> arguments&nbsp;&nbsp;&nbsp; 返回该函数执行时内置的arguments对象。
>
> caller&nbsp;&nbsp; 返回调用当前函数的函数。
>
> constructor&nbsp;&nbsp; 返回创建该对象的构造函数。
>
> length&nbsp; 返回函数定义的参数个数。
>
> prototype&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回创建该对象的函数的原型对象

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style="color:red">arguments</span><span style="color:red">属性进一步理解：</span>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; arguments属性是<span style="color:red">正在执行的</span>函数的内置属性，返回该函数的arguments对象。arguments对象包含了调用该函数时所传入的实际参数信息(参数个数、参数&#20540;等)。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; arguments对象有以下三个属性：

&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; length属性，&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回实际传入的参数个数。

&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; caller属性，&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回调用当前函数的函数，&#20540;为Function对象。

&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;0...n属性，&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 以顺序索引访问传入的具体参数。例如，使用arguments[0]可以访问传入的第1个参数，arguments[1]可以访问传入的第2个参数。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 注：arguments对象具有length属性和0...n属性，看起来与数组的访问方式相同，但arguments并不是数组，它没有数组对象所具备的其他成员属性和方法。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 代码举例：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style="white-space:pre"></span>

<pre name="code" class="javascript">function test(){
document.writeln(&quot;实际传入的参数个数：&quot; +arguments.length); // 实际传入的参数个数：3
    /* &quot;test.&quot;可以省略 */
    for(var i = 0; i &lt;test.arguments.length; i++){
        document.writeln(&quot;传入的第&quot; + (i + 1)+&quot;个参数：&quot; + arguments[i]);
    }
    // 传入的第1个参数：1 传入的第2个参数：张三 传入的第3个参数：true
    // callee属性返回的就是当前函数
    document.writeln( arguments.callee === test); // true
};
test(1, &quot;张三&quot;, true);</pre>

&nbsp;

### 3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象方法

> 方法&nbsp;&nbsp;&nbsp; &nbsp;&nbsp; 描述
>
> apply() &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 调用当前Function对象，可同时改变函数内的this指针引用，函数参数以数组或arguments对象的形式传入。
>
> call()&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 调用当前Function对象，可同时改变函数内的this指针引用，函数参数一个个分别传入。
>
> toString()&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回定义该Function对象的字符串。
>
> valueOf()&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回Function对象本身。

&nbsp;

> <span style="color:#ff0000">call ()方法进一步理解：</span>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; call()函数用于调用当前函数functionObject，并可同时使用指定对象thisObj作为本次函数执行时函数内部的this指针引用。

> > 1.语法: functionObject.call( [ thisObj [, arg1 [, arg2 [, args...]]]] )
>
> > 2.参数：
>
> > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 参数 描述
>
> > thisObj&nbsp; 可选/Object类型指定执行functionObject函数时，函数内部this指针引用的对象。
>
> > arg1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可选/任意类型调用functionObject函数时传入的第1个参数。
>
> > arg2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可选/任意类型调用functionObject函数时传入的第2个参数。
>
> > args&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可选/任意类型调用functionObject函数时传入的更多参数，可以有多个。
>
> > 注：如果为该函数所属的functionObject对象提供了传入参数，则必须提供thisObj参数。
>
> > 3.代码举例：
>
> > <span style="white-space:pre"></span>
> >
> > <pre name="code" class="javascript"> var obj = {name:&quot;李四&quot;, age: 20};
> >                 function foo(a, b){
> >                             document.writeln(this.name);   
> >                             document.writeln(a);   
> >                             document.writeln(b);   
> > }
> > // 改变this引用为obj，同时传递两个参数
> > foo.call(obj, 12, true); // 李四 12 true</pre>
> >
> > &nbsp; &nbsp; &nbsp; &nbsp;
> <span style="color:#ff6666">apply ()方法进一步理解：</span>
>
> &nbsp;apply()函数用于调用当前函数functionObject，并可同时使用指定对象thisObj作为本次函数执行时函数内部的this指针引用。call()函数是将Function对象的参数一个个分别传入，apply()函数是将Function对象的参数以一个数组或arguments对象的形式整体传入。
> > 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;语法：functionObject.apply( [ thisObj [, argsArray ]] )
>
> > 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数：
>
> > 参数&nbsp;&nbsp; 描述
>
> > thisObj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可选/Object类型指定执行functionObject函数时，函数内部this指针引用的对象。
>
> > argsArray&nbsp;&nbsp;&nbsp; 可选/Array|argumens对象调用functionObject函数时所传入的参数数组或arguments对象。

<span style="white-space:pre"></span>注：如果提供了argsArray参数，则该参数必须是一个数组，或者arguments对象。数组中的每个元素(arguments对象中的每个属性0...n)将按照顺序作为参数传入该函数。如果提供了argsArray参数，则必须提供thisObj参数。

### <span style="color:#ff0000">4．Function对象使用难点之闭包。</span>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 闭包（closure）：闭包，就是在function对象内部return 一个内嵌方法，该内嵌方法中操作着对象中的局部变量（私有属性），在外部通过该Function对象实际控制了该局部变量。好处就是减少了全局变量的使用以及其引起的命名空间的冲<span style="white-space:pre"></span>&nbsp; &nbsp;突。

<span style="white-space:pre"></span>&nbsp; &nbsp;看代码：

> <pre name="code" class="javascript">var add = (function () {
>     var counter = 0;
>     return function () {return counter += 1;}
> })();
>
> add();
> add();
> add();
> // 计数器为 3</pre>

> 即add= function () {return counter &#43;= 1;}，那么add就是该Function对象的引用（<span style="color:red">注意并不是自调用的函数的对象，自调用的</span><span style="color:red">Function</span><span style="color:red">对象只运行一次，但是自调用的</span><span style="color:red">Function</span><span style="color:red">对象在内存中依然存在），</span>通过add（）调用return的Function对象，从而对自调用Function对象中的counter私有属性产生影响。这就是闭包。

## 九、&nbsp;Object对象

首先，object是一种数据类型，而Object作为一种对象，是object数据类型中的一种。

&nbsp;

Object对象，是JS中所有对象的基对象，包括以上的所有对象，类&#20284;于java中的Object基类的概念。Object对象主要用于将任意数据封装成对象形式。

以上的所有对象都是对于Object对象的扩展，添加了属性和方法。

### 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;创建对象

> 用法一：充当Object对象的构造函数使用&nbsp;&nbsp; new Object( [value ] )
>
> 用法二：当作普通函数使用，其行为与用法一(使用new关键字)完全一致&nbsp;&nbsp;&nbsp; Object([ value ] )&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;

> Object()将会根据参数value的数据类型，返回对应类型的对象：
>
> &nbsp;如果value为基元数据类型&quot;Boolean&quot;、&quot;Number&quot;、&quot;String&quot;，则返回对应类型的对象，例如：Boolean对象、Number对象、String对象。
>
> &nbsp;如果value本身为对象，则不对其作任何更改，返回其本身。
>
> &nbsp;&nbsp;&nbsp;&nbsp;如果省略了value参数，或value为null、undefined，则返回自身无任何属性的Object对象。
> 代码举例：
> <pre name="code" class="javascript">// 基元数据类型 =&gt; 对应类型的对象
> var strObj = new Object( &quot;CodePlayer&quot; ); // 返回一个String对象，相当于newString(&quot;CodePlayer&quot;);
> var numObj = new Object( 18 ); // 返回一个Number对象，相当于new Number(18);
> var boolObj = new Object( true ); // 返回一个Boolean对象，相当于new Boolean(true);
> document.writeln( strObj instanceof String ); // true
> document.writeln( numObj instanceof Number ); // true
> document.writeln( boolObj instanceof Boolean ); // true</pre>
> <pre name="code" class="javascript">// 对象 =&gt; 对象本身
> var arr = [ 2, 3, 5];
> var regex = /^\d$/;
> function test(){
>     alert(&quot;HelloWorld!&quot;);
> }
> var arrObj = new Object( arr );
> var regObj = new Object( regex );
> var funObj = new Object( test );
> document.writeln( arrObj === arr ); // true
> document.writeln( regObj === regex ); // true
> // 虽然typeof funObj返回的是&quot;function&quot;，但它本身就是一个Function对象
> document.writeln( funObj === test ); // true</pre>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

> <pre name="code" class="javascript">// null =&gt; 空对象
> var obj = new Object( null );
> document.writeln( obj instanceof Object ); //true</pre>
> 用法三：以字面&#20540;形式创建一个自定义对象：{ property1:value1, property2:value2,propertyN:valueN }
> <pre name="code" class="javascript">// 将上述自定义对象obj以字面值形式声明
> var o = {
>     // 所有的属性名称都可以加上引号
>     name: &quot;CodePlayer&quot;,
>     age: 18,
>     sayHi: function(){
>         alert(&quot;HelloWorld!&quot;);
>     },
>     &quot;foo-bar&quot;: &quot;包含特殊字符&quot;
> };</pre>

### 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象的属性

> 属性&nbsp;&nbsp;&nbsp; 描述
>
> constructor&nbsp;&nbsp; 返回创建该对象的构造函数
>
> prototype&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回创建该对象的函数的原型对象

### 3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象的方法

> 方法 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> hasOwnProperty(x)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指示对象是否具有指定名称的属性。
>
> isPrototypeOf(x) 指示对象是否存在于另一个对象的原型链中。
>
> propertyIsEnumerable(x)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指示指定属性是否为对象的一部分以及该属性是否是可枚举的。
>
> toLocaleString()&nbsp; 以字符串的形式返回&#20540;，该&#20540;适合于宿主环境的当前区域设置。
>
> toString()&nbsp;&nbsp; 返回表示对象的字符串。
>
> valueOf()&nbsp;&nbsp; 返回对象的原始&#20540;。

### 4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象的属性和方法的动态操作

所有基于Object对象的对象都支持expando属性。

> 1)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Object对象不同于以上的内置对象，它的属性和方法可以动态添加、修改和删除（有些内置属性和方法除外）。
> 代码举例：
> > <pre name="code" class="javascript"> var obj = newObject();
> > obj.name = &quot;CodePlayer&quot;;
> > obj.age = 18;
> > obj.sayHi = function( ){
> >     alert(&quot;HelloWorld!&quot;);
> > };
> > document.writeln( obj.age ); // 18
> >
> > // 移除age属性
> > delete obj.age;
> > document.writeln( obj.age ); // undefined</pre>
> 2)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在JS中对象的属性可以通过两种方式访问：object.property和object[&quot;property&quot;]。
> 代码举例：
> > <pre name="code" class="javascript">var obj = newObject();
> > obj.name = &quot;CodePlayer&quot;;
> > obj.age = 18;
> > obj.sayHi = function( ){
> >     alert(&quot;HelloWorld!&quot;);
> > };
> >
> > // 包含特殊字符的属性只能以此方式访问
> > obj[&quot;foo-bar&quot;] = &quot;包含特殊字符&quot;;
> >
> > document.writeln( obj.age ); // 18
> > document.writeln( obj[&#39;age&#39;] ); // 18
> > document.writeln( obj[&quot;foo-bar&quot;] );// 包含特殊字符e</pre>

十、&nbsp;Error对象

Error对象主要用于存储JS中错误或异常的相关描述信息。

### 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象属性

> 属性&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> constructor&nbsp;&nbsp;&nbsp; 返回创建该对象的构造函数。
>
> message&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回错误或异常的相关描述信息。
>
> name&nbsp;&nbsp;&nbsp; 返回错误或异常的类型名称。
>
> prototype&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回创建该对象的函数的原型对象

### 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对象方法

> 方法 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 描述
>
> toString()&nbsp;&nbsp; 返回包含相关错误信息的字符串。

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

<span style="color:red">说明：</span>

<span style="color:red">1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:red">所有的对象都有自己的构造方法，在</span><span style="color:red">new</span><span style="color:red">时其实就是调用了自身的构造方法创建对应的对象。该方法在上面的对象方法列表中没有写出来</span>

<span style="color:red">2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:red">在创建对象时很多都是没有</span><span style="color:red">new</span><span style="color:red">关键字而直接使用方法创建，只是调用了一个普通的方法，因此返回的并不是对象，而是一个简单的基础类型，本质和</span><span style="color:red">3</span><span style="color:red">相同。该方式只存在于三个有基础数据类型对应的对象类型，包括</span><span style="color:red">String</span><span style="color:red">、</span><span style="color:red">Boolean</span><span style="color:red">、</span><span style="color:red">Number</span><span style="color:red">。以及</span><span style="color:red">Array</span><span style="color:red">对象、</span><span style="color:red">Function</span><span style="color:red">对象和</span><span style="color:red">Object</span><span style="color:red">对象中。</span>

<span style="color:red">3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:red">字面量形式，只存在于三个有基础数据类型对应的对象类型，包括</span><span style="color:red">String</span><span style="color:red">、</span><span style="color:red">Boolean</span><span style="color:red">、</span><span style="color:red">Number</span><span style="color:red">。以及</span><span style="color:red">Array</span><span style="color:red">对象、</span><span style="color:red">Function</span><span style="color:red">对象和</span><span style="color:red">Object</span><span style="color:red">对象中。</span>

&nbsp;

以上部分参考：[http://www.365mini.com/page/tag/javascript-function-object](http://www.365mini.com/page/tag/javascript-function-object)。

发现一篇声明变量的五种方式的好文章，有助于理解创建不同类型的变量：[http://www.jb51.net/article/34191.htm](http://www.jb51.net/article/34191.htm)。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;

&nbsp;

附：

## **1.instanceof 运算符**

**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#26684;式：x&nbsp; instanceof&nbsp;y ：**

> **含义：X是否是y类型，返回&#20540;为boolean。如果x在对象y的原型链 (prototype chain) 中被发现，那么instanceof操作符将返回true，否则返回false.**
>
> 在使用 typeof 运算符时采用引用类型存储&#20540;会出现一个问题，无论引用的是什么类型的对象，它都返回 &quot;object&quot;。ECMAScript 引入了另一个<span style="color:red"> Java</span><span style="color:red">运算符</span><span style="color:red"> instanceof</span> 来解决这个问题。
>
> instanceof 方法要求开发者明确地确认对象为某特定类型。例如：
> > <pre name="code" class="javascript">var oStringObject =new String(&quot;hello world&quot;);
> > alert(oStringObjectinstanceof String);          //输出 &quot;true&quot;
> >
> >  varuw3c=new Function()
> > console.log(testinstanceof(uw3c))//true
> >   console.log(test instanceof(Function))//false
> > console.log(uw3c instanceof(Function))//false
> > console.log(test instanceof(Object))//true
> >
> >   console.log(Functioninstanceof(Object))//true
> >   console.log(Objectinstanceof(Function))//true
> >
> >   console.log(Array instanceof(Function))//true
> >   console.log(Stringinstanceof(Function))//true
> >   console.log(Functioninstanceof(Function))//true</pre>
> 发现：&nbsp;&nbsp;&nbsp;&nbsp; 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 对象的实例属于对象的类型或者是Object对象类型，却不属于Function对象类型，
>
> <span style="white-space:pre"></span>2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 内置对象（包括Object对象）都属于Function对象类型，但是Function对象也属于Object对象类型，也就是所有内置对象(包括Object和Function对象本身)既属于Function对象类型，也属于Object对象类型

<span style="color:red">&nbsp;</span>

## **2.JS的基础类型与引用类型**

**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **ECMAScript变量包含两种不同类型的&#20540;：基本类型&#20540;、引用类型&#20540;；

> 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基本类型&#20540;：指的是保存在栈内存中的简单数据段；
>
> 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;引用类型&#20540;：指的是那些保存在堆内存中的对象，意思是，变量中保存的实际上只是一个指针，这个指针执行内存中的另一个位置，由该位置保存对象；
>
> 两种访问方式：
>
> 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基本类型&#20540;：按&#20540;访问，操作的是他们实际保存的&#20540;；
>
> 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;引用类型&#20540;：按引用访问，当查询时，我们需要先从栈中读取内存地址，然后再顺藤摸瓜地找到保存在堆内存中的&#20540;；
>
> ![]()

<span style="white-space:pre"></span>注意图中的Number、Boolean、Null、String、Undefined都是基础类型，不是代表的对象

> 两种类型复制：
>
> 1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基本类型变量的复制：从一个变量向一个变量复制时，会在栈中创建一个新&#20540;，然后把&#20540;复制到为新变量分配的位置上；
>
> 2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;引用类型变量的复制：复制的是存储在栈中的指针，将指针复制到栈中未新变量分配的空间中，而这个指针副本和原指针执行存储在堆中的同一个对象；复制操作结束后，两个变量实际上将引用同一个对象；因此改变其中的一个，将影响另一个；
>
> ![]()
>
> <span style="color:red">两种变量类型检测</span>
>
> <span style="color:red">1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:red">Typeof</span><span style="color:red">操作符是检测基本类型的最佳工具；</span>
>
> <span style="color:red">2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:red">Instanceof</span><span style="color:red">用于检测引用类型，可以检测到具体的，它是什么类型的实例；</span>

**&nbsp;**

**<span style="white-space:pre"></span>以上部分内容来源于：**[**http://blog.sina.com.cn/s/blog_6fd4b3c10101d0va.html**](http://blog.sina.com.cn/s/blog_6fd4b3c10101d0va.html)**。**

## **3.constructor属性详解**

**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **每个对象都有一个属性constructor，该属性<span style="color:red">以字符串形式</span>返回对应对象的构造方法。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 代码举例：

> <pre name="code" class="javascript">function employee(name,job,born) {
> this.name=name;
> this.job=job;
> this.born=born;
> }
> var bill=new employee(&quot;BillGates&quot;,&quot;Engineer&quot;,1985);
> document.write(bill.constructor);
>
> 输出：
> function employee(name, job, born) {this.name = name;this.jobtitle = job; this.born = born;}</pre>

&nbsp;

## **4.prototype属性详解**

**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **prototype叫做原型，官方说法是：返回对象类型原型的引用。

_<span style="color:#00B0F0">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="color:#00B0F0">有文档</span>_

> 特别说明：
>
> <span style="color:#0D0D0D">1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>关于类与对象这个概念的申明：
>
> <span style="color:red">Js</span><span style="color:red">中没有类的概念，对比</span><span style="color:red">java</span><span style="color:red">，</span><span style="color:red">java</span><span style="color:red">中的类对应</span><span style="color:red">js</span><span style="color:red">的对象，</span><span style="color:red">java</span><span style="color:red">中的对象</span><span style="color:red">/</span><span style="color:red">实例对应</span><span style="color:red">js</span><span style="color:red">中的对象实例。在</span><span style="color:red">
>
>  ECMA-262 </span><span style="color:red">中根本没有出现“类”这个词。</span><span style="color:red">ECMAScript</span><span style="color:red">定义了“对象定义”，逻辑上等价于其他程序设计语言中的类。</span>
>
> <span style="color:#0D0D0D">2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>方法和函数不是一回事
>
> <span style="color:red">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="color:red">函数是一个</span><span style="color:red">Function</span><span style="color:red">对象，具有相应的属性和方法，而方法内置于各种对象中，只是为了完成相应的功能而已</span>
>
> **<span style="color:#0D0D0D">3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:red">区分以下五者的区别：</span>**

**<span style="color:red">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>**

> **<span style="color:#0D0D0D">1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">Function</span>**
>
> **<span style="color:#0D0D0D">2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">function</span>**
>
> **<span style="color:#0D0D0D">3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">var x =function</span><span style="color:#0D0D0D">（）</span><span style="color:#0D0D0D">{ }</span>**
>
> **<span style="color:#0D0D0D">4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">var x = new Function</span><span style="color:#0D0D0D">（）</span>**
>
> **<span style="color:#0D0D0D">5.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">var xx = new x</span><span style="color:#0D0D0D">（）</span>**
>
> <span style="color:#0d0d0d">**说明：**</span>
> **<span style="color:#0D0D0D">1.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">是作为一个内置对象，直接使用：</span><span style="color:#0D0D0D">Function.prototype</span>**
>
> **<span style="color:#0D0D0D">2.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">作为一个关键字，用于创建自建</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象，也用于创建对象中的方法</span>**
>
> **<span style="color:#0D0D0D">3.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">字面量形式创建自建</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象，也可作为一般的方法，使用</span><span style="color:#0D0D0D">x</span><span style="color:#0D0D0D">（）执行该方法，</span><span style="color:#0D0D0D">x</span><span style="color:#0D0D0D">为引用类型</span>**
>
> **<span style="color:#0D0D0D">4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">构造方法形式创建自建对象</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">，</span><span style="color:#0D0D0D">x</span><span style="color:#0D0D0D">为引用类型，指向该自建对象</span>**
>
> **<span style="color:#0D0D0D">5.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">创建自建对象</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">的一个实例，</span><span style="color:#0D0D0D">x</span><span style="color:#0D0D0D">为正常的</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象（引用），</span><span style="color:#0D0D0D">xx</span><span style="color:#0D0D0D">为该对象的一个实例，拥有对象的属性和方法对应的实际意义的&#20540;，它的内容的改变不能影响对象的内容。</span>**
>
> **<span style="color:red">特别注意：创建实例，肯定是自建对象类型。而对应的自建对象却必须是</span><span style="color:red">Function</span><span style="color:red">对象类型，其他所有自建对象类型都不可以创建实例！这也是</span><span style="color:red">Function</span><span style="color:red">对象很特殊的一点。</span>**
>
> **<span style="color:red">测试：</span>**
>
> <pre name="code" class="javascript">var uw3c = newObject()
> var test = newuw3c();//Uncaught TypeError: uw3c is not a function</pre>

## **<span style="color:#0D0D0D">4.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#0D0D0D">对</span><span style="color:#0D0D0D">Function</span><span style="color:#0D0D0D">对象的实例进一步分析</span>**

> <pre name="code" class="javascript">var uw3c=new Function()
> uw3c. myname=&quot;myname&quot;
> uw3c.myfunc=function(){alert(&quot;myfunc&quot;)}
> uw3c.prototype.propname=&quot;propname&quot;
> uw3c.prototype.propfunc=function(){alert(&quot;propfunc&quot;)}
> var test = newuw3c();
>  test.func=function(){alert(&quot;testfunc&quot;)}
> console.log(typeof test);//object
>   console.log(testinstanceof(Function));//false
>  console.log(test instanceof(Object));//true
>
> console.log(test. myname);//undefined
>  test.myfunc()//UncaughtTypeError: test.myfunc is not a function
>
> console.log(test. propname);//propname
>  test.propfunc()//propfunc
> test. func()//func</pre>

<span style="color:#0D0D0D">&nbsp;</span>

> <span style="color:red; background:#D9D9D9">测试发现：</span><span style="color:#00B050; background:#D9D9D9">Function</span><span style="color:#00B050; background:#D9D9D9">对象的实例的类型为</span><span style="color:#00B050; background:#D9D9D9">object</span><span style="color:#00B050; background:#D9D9D9">类型的</span><span style="color:#00B050; background:#D9D9D9">Object</span><span style="color:#00B050; background:#D9D9D9">对象。而不是</span><span style="color:#00B050; background:#D9D9D9">Function</span><span style="color:#00B050; background:#D9D9D9">对象</span><span style="color:red; background:#D9D9D9">。且在</span><span style="color:red; background:#D9D9D9">new
>
>  uw3c()</span><span style="color:red; background:#D9D9D9">时候会执行</span><span style="color:red; background:#D9D9D9">uw3c()</span><span style="color:red; background:#D9D9D9">。因为是</span><span style="color:red; background:#D9D9D9">Object</span><span style="color:red; background:#D9D9D9">对象，与原来的</span><span style="color:red; background:#D9D9D9">Function</span><span style="color:red; background:#D9D9D9">对象没有关系了，所以</span><span style="color:red; background:#D9D9D9">Function</span><span style="color:red; background:#D9D9D9">对象的属性和方法就自然访问不到了，后加给实例的属性和方法本质上是加到</span><span style="color:red; background:#D9D9D9">Object</span><span style="color:red; background:#D9D9D9">对象中去了。这里涉及到原型，将在原型中具体讲解。</span>

<span style="color:red">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; console.log(test.__proto__== uw3c.prototype)//true</span>

> <span style="color:red; background:#D9D9D9">创建</span><span style="color:red; background:#D9D9D9">Function</span><span style="color:red; background:#D9D9D9">对象的实例的本质是：</span><span style="color:red; background:#D9D9D9">test.__proto__ = uw3c.prototype</span><span style="color:red; background:#D9D9D9">。</span>

<span style="color:red; background:#D9D9D9">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; test</span><span style="color:red; background:#D9D9D9">为</span><span style="color:red; background:#D9D9D9">Object</span><span style="color:red; background:#D9D9D9">对象，</span><span style="color:red; background:#D9D9D9">uw3c</span><span style="color:red; background:#D9D9D9">为</span><span style="color:red; background:#D9D9D9">Function</span><span style="color:red; background:#D9D9D9">对象，两者的联系不是他们的属性和方法，只是在创建实例的时候产生了实例的</span><span style="color:red; background:#D9D9D9">Object</span><span style="color:red; background:#D9D9D9">对象的</span><span style="color:red; background:#D9D9D9">__proto__</span><span style="color:red; background:#D9D9D9">属性赋&#20540;了原</span><span style="color:red; background:#D9D9D9">Function</span><span style="color:red; background:#D9D9D9">对象的</span><span style="color:red; background:#D9D9D9">prototype</span><span style="color:red; background:#D9D9D9">属性。</span>

<span style="color:red">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="color:red">这样产生一个问题：当实例的</span><span style="color:red">Object</span><span style="color:red">对象被赋&#20540;的属性和方法和原</span><span style="color:red">Function</span><span style="color:red">对象的</span><span style="color:red">proptype</span><span style="color:red">属性储存的属性和方法名称一样怎么办：</span>

> <pre name="code" class="javascript">var uw3c=new Function()
> uw3c.prototype.propname=&quot;propname&quot;
>  uw3c.prototype.propfunc=function(){alert(&quot;propfunc&quot;)}
>   var test = new uw3c();
>   test.propname=&quot;testpname&quot;
>  test.propfunc=function(){alert(&quot;testfunc&quot;)}
>
>   console.log(test.propname);//testpname
>   test.propfunc()//testfunc</pre>

> 测试发现：被赋&#20540;到实例的Object对象的属性和方法覆盖了__proto__属性里的属性和方法。想想也是，__proto__属性的内的属性和方法原本就可以被实例直接访问，也就相当于是实例的属性和方法了， 当被新赋&#20540;一样的名称时候，肯定会被覆盖了

            <div>
                作者：z893196569 发表于2015/9/26 16:08:14 [原文链接](http://blog.csdn.net/z893196569/article/details/48685961)
            </div>
            <div>
            阅读：68 评论：0 [查看评论](http://blog.csdn.net/z893196569/article/details/48685961#comments)
            </div>
