---
title: 'js数据类型'
tags:
-
categories:
- Javascript
date: 2015-09-23 19:09:37
---

按照spec，JS的数据类型就是以下六种：

**<span style="color: red">5种基本数据类型+1种object类型（ES6后多了一个symbol类型，此处不阐述）</span>**

### 1.undefined
```
alert(undefined);//"undefined"
alert(typeof undefined);//"undefined"
alert(undefined instanceofObject);// "false"
alert(undefined instanceofundefined);// 语法错误：instanceof不能对undefined运算
alert(undefined instanceofUndefined);// 错误："Undefined"未定义
```
<!-- more -->
>undefined作为一种基本数据类型，也是js里内置的一个变量，该变量的值就是“undefined”，并且该变量根据typeof判断出本身属于undefined数据类型

```
使用：// 如何判断一个变量是否声明
alert(typeof x =="undefined");// true
alert(typeof x==undefined);//false
```
>undefined是一个undefined类型的变量，它的值为“undefined”，而正常的“undefined”是一个string类型的变量，两者不等。typeof操作符返回的是字符串“undefined”

### 2.null
```
alert(null);//"null"
alert(typeof null);//"object"
```
>和undefined很相似：null作为基本的数据类型，也有一个内置的变量null，它的值为“null”，
typeof null的返回值“object”是ECMA-262中规定的内容。并且这规定只是为了兼容性，实际上null并不是一个Object的实例。现在比较普遍的认知是，typeof null返回“object”是一个历史错误（JS的发明者Brendan Eich自己也是这样说的），只是因为要保持语言的兼容性而维持至今。从ES5制定开始就有动议将typeof null改为返回“null”（如启动node加上“--harmony_typeof”参数，即是如此），但是当前ES6标准草案仍然维持了原样。

**null** 和 **undefined** 的区别：
```
alert(null==undefined);//"true"
alert(null===undefined);// "false"
```
>JS解释器一般认为null和undefined是相等的，虽然在严格等于运算时结果是false。（据说这是为了兼容以往的浏览器中没有undefined而设的。）
undefined是作为Global对象的属性存在的，而null则是ECMA规范中设定的一个字面值。换句话说，undefined是存放在Global中的属性（所以像单态），而null是解释执行时产生的值。

```
alert(undefined==0);//"false"
alert(null==0);// "false"
```
>和其他语言不同，他们和0值是不相等的

### 3.boolean
```
var x=true;
alert(x);// "true"
alert(typeof x);// "boolean"
alert(!x==0);// "true"
alert(x==1);// "true"
alert(x==2);// "false"
```
>boolean并不是一个变量，它只是很普通的基本数据类型。true和1相等，false和0相等，但是他们不能转换成1和0

###  4.number
```
varx=5;
alert(x/2);// "2.5"
```
>JS会把所有数字型的数据解释成浮点数，所以没有short,int,long,float,double等类型区分

```
alert(10);// "10"
alert(010);// "8"
alert(0x10);// "16"
```

>支持各种进制：
1. 十进制：无须任何修饰，而且能定义小数。
2. 八进制：需以0开头，但必须注意的是，后续的数字不能大于7，不然还是会被判断为十进制数字面值的。八进制数能表示负值，但不能表示小数。
3. 十六进制：以0x或0X开头，后续数字为符合十六进制表示法的0-9或a-f的大小写字母。同样地，十六进制数能表示负值，但不能表示小数。

另外，对于数字型的数据，有以下几个特殊值：
1. NaN（not a number），意思不是一个数，但它却是数字型的一个值，当对不适当的数据进行数学运算时，例如字符串或未定义值，它将会作为运算结果返回。NaN不与任何值相等，包括它自己，但我们可以使用方法isNaN来判定一个值得是否NaN。
2. Infinity，意思是无穷大，相对地，有负无穷大-Infinity。当一个数大于等于21024或小于等于21024，会分别用他们的正负形式来表示。所有Infinity是相等的，当然，区分正负地相等。

### 5.string
```
alert('How "test"things go on?');
alert('That/'test/' sounds great!');
```

由于JS没有单字符的数据类型——如Java中的char，所以单双引号的成对使用时基本不存在区别——Java中单引号里的是单字符。而且单双引号能互相嵌套使用，但单（双）引号必须包含所有双（单）引号，并且双（单）引号中不能再出现单（双）引号。另一种可以使单（双）引号都能嵌套自身的方法是使用转义符“/”。

	alert("/u0059/u0065/u0073");//"Yes"


>string支持unicode字面值，他们以并且只能以“/u”开头，后面跟四位的unicode编码（不区分大小写）。

### 6.object

object是一种数据类型，它的结构是一个对象结构。不可与Object对象混淆。
在ECMA规范对其类型进行划分如下：
1. **宿主对象（Host Object）**
指依赖于宿主环境存在的对象，例如所有浏览器中的window（BOM）和document（DOM）对象。所有不是本地对象的对象都是宿主对象。
有文档
2. **本地对象（Native Object）**
指独立于宿主环境存在的对象，分为内置对象和用户自建对象，标准的本地对象是**Global,Math,Object,Function,Number,Boolean,String,Array,Date,Math,RegExp和各种Error对象**，非标准的本地对象则是指自建对象，需要自己去创建{k-v}；
    1. 内置对象（Build-in Object）：包括Global,Math,Object,Function,Number,Boolean,String,Array,Date,RegExp以及Error错误对象。这些对象有已定义的属性和方法，可以直接使用关键字如Function访问它们的属性和方法，而不需要new一个对象出来。
    2. 自建对象：分为两种创建方式：
       1. 字面量形式创建：Object对象：var x ={k：v，K：v…}
String对象：var x =“xx”
注意：本质上并没有创建对象，只是可以和对象一样正常使用

	  2. 运用内置对象的构造方法new出自定义的对应类型的对象（内置对象中Global、Math静态对象除外，不可new）。比如：
```
var a = new Object（） ；
var b =new Function（）；
```
a为自建对象Object的引用，和内置对象拥有同样的内容，区别是它需要new

>以上大部分参考自[链接](http://blog.csdn.net/natineprince/article/details/4787689)。


### 附：
#### typeof 运算符：
    1.typeof xx
    2.typeof（xx）
>当xx是基本数据类型时返回xx的具体的基本数据类型的字符串(特殊：typeof null  //object)
>当xx是某一个Object类型比如Array，返回“object”(特殊：typeof func  //function)

**特别说明：**
<span style="color: red">
function并不是一种单独的数据类型，至少官方spec不这样认为，注意和Function对象不要混淆，Function是object类型中的一种内置对象，和Array的性质一样，但是却灵活的多。并不能因为typeof返回值为function就将其作为一种数据类型，就像null的typeof返回object而不能将其归并为object一样【按照spec，typeof只是一个运算符，其返回值并不能作为JS类型系统的依据】. object类型中包含内置的Object对象，该对象是所有内置对象和自建对象的母版，包括自身。
</span>
