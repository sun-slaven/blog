---
title: 《你不知道的JavaScript》
tags:
  - javascript
categories:
  - 技术书籍笔记
date: 2017-02-17 17:25:08
---
# 第一部分 作用域和闭包
## 第一章 作用域是什么

状态的定义： 存储并访问、修改变量的值的能力。
Javascript 被称为“动态”或者是“解释执行”语言，但是它其实是一门“编译”语言。
### 编译语言在编译期间的三个经历步骤：
1. 分词/词法分析（Tokenizing/Lexing）
var a = 2 ，会将代码分解成词法单元（token）， "var、a、=、2、；"，
整个过程叫分词，但是依据什么规则进行分词，这个过程叫词法分析。
2. 解析/语法分析（Parsing）
将分词以数组作为单位，转换为一个“抽象语法树”（AST）。
3. 代码生成
将AST转化为一组机器指令（最终的代码），所以这个过程就与平台相关。
如 var a = 2，转换的机器指令若执行，会先创建一个a变量（分配内存），然后将2赋值给a。

### 引擎、编译器、作用域的关系
* 引擎：负责整个程序的编译以及执行。执行编译器生成的代码时，会通过相应的查找类型在作用域中查询变量。
* 编译器：编译期间与引擎合作，负责通过语法分析来解析以及代码生成。实际这些“编译”的活都是它干了，过程中会和作用域沟通，完成变量的声明过程。
* 作用域：与引擎合作，负责收集并维护所有声明的变量组成的一系列查询，并实施一套非常严格的规则，依此确定当前执行的代码对变量的访问权限。
引擎的查找类型
* LHS查询：左侧查询。代表赋值操作的左侧。会试图找到变量的容器，从而进行赋值。非严格模式下，若找不到，引擎会自动在全局作用域下隐式声明一个变量并赋值。ES5的严格模式禁止了这样的行为。
* RHS查询： 右侧查询。代表非左侧。直接查找某个变量的值。

若引擎查询相应的变量时发现未声明或者未找到，则会报相应的异常（ReferenceError、TypeError等）。举例：
```
function foo(a){
    console.log(a);
}

foo(2);
```
首先，编译器会先完成对foo函数，局部变量a的声明。然后引擎会执行编译好生成的代码（先忽略function的声明，执行foo(2)），引擎先通过作用域进行RHS查询foo变量，发现有注册之后去执行foo，发现要将2赋值给局部变量a，先进行LHS查询a是否已经声明并赋值，然后进行RHS查询console变量，再RHS查询log方法，再RHS查询变量a，然后LHS查询log方法里的局部变量...。

注： 编译器会首先完成所有变量的声明解析（也就是变量声明提升）。然后javascript引擎会逐行的先让编译器进行编译然后运行编译器产生出的代码，即编译后就立马运行。这是和java等编译语言不同的地方。

## 第二章 词法作用域

在编译器进行词法阶段的时候，变量和块写在哪里决定了它们的作用域。这就是词法作用域。
遮蔽效应： 在作用域内查找相应的标识符时，内部的标识符“遮蔽”了外部相同的标识符。

### 欺骗词法：
1. eval(str)：接受一个字符串，在相应位置将str转换为语句执行，用于执行一段动态生成的字符串代码。字符串的作用域就是eval所在语句的作用域。严格模式下，eval会创建自己的一个作用域，即str的作用域是eval所在的作用域的子域。
2. with:   with(obj){
    a = 3;
    b = 4;
}
本质是LHS查询obj，查询到obj.a则进行赋值。查询不到则有可能会将b暴露在全局对象下（帮助创建变量），所以不是将当前的上下文改为obj。严格模式下禁止使用。
使用欺骗词法会对性能产生很大的影响，因为js引擎会在编译阶段进行数项的性能优化，有些优化依赖于能够根据代码的词法进行静态分析，并预先确定所有变量和函数的定义位置，然后在执行过程中快速找到标识符。但是如果引擎发现eval和with，就无法做静态分析。因此，不推荐使用这两个关键字。

## 第三章 函数作用域和块作用域

### 函数作用域

函数作用域的作用： 最小暴露原则，在软件设计过程中，应该最小限度的暴露必要内容，而将其他内容都隐藏起来，比如某个模块或对象的API设计。具有封装性和隐蔽性。也避免了过多的变量暴露到全局，造成声明冲突。

这个思想被普遍用于第三方插件和库，他们往往只暴露一个全局的命名空间，属性和方法放在该命名空间的对象下。
利用函数作用域，使模块管理成为可能。
函数作用域是js中最常见的作用域单元。
IIFE：立即调用函数表达式：
```
(function(global){
    xx
})(window)

或者：

(function(def){
    def(window)
})(function def(global){
    xx
})
```
前面（）内的内容叫函数表达式。xx产生一个新的函数作用域
块作用域

with关键字其实提供的也是一个块作用域。

try/catch： es3中规定的该结构中catch其实也会创建一个块作用域

ES6的let关键字可以将变量绑定到相应的块作用域中，同时不允许该变量声明提升。

for循环中，i变量要用let声明，避免var的形式造成全局污染。

### 第四章 提升

提升过程中，函数声明会比变量提升优先。
重复的var变量声明会被忽略，但是重复的函数声明会覆盖前面的。

声明提升，并不是全部都提升到全局作用域的顶部，而是提升到自身所在的作用域的顶部。

### 第五章 作用域闭包

闭包定义：通过某种手段将持有之前包裹的外部作用域的内部函数传递到所在的词法作用域之外（不一定在上层），这个内部函数就实现了闭包。若执行这个函数，就使用了闭包。技术上将，闭包是发生在定义时。

闭包和局部作用域有没有局部变量没有任何关系，闭包并不是指的形式上，重点在始终持有声明所处的词法作用域。

闭包的好处：闭包可以使得函数可以继续访问定义时的词法作用域。所谓的模块机制都是使用了闭包。

块作用域+闭包 = 天下无敌

实例：
```
function foo(){
    var a = 2;
    function baz(){
        console.log(a);
    }
    return baz;
}

var baz = foo();
baz();//闭包

function foo(){
    var a = 2;
    function baz(){
        console.log(a);//会始终保留对foo函数作用域的访问权，所以此处的作用域一直都不会销毁，所以闭包太多会引起内存问题
    }
    bar(baz);
}

function bar(fn){
    fn()//这就是闭包
 }
```
一般我们使用的ajax，定时器，事件监听器或者其他任何的异步过程中使用的回调函数，其实就是在使用闭包，因为回调函数可以访问当前的作用域，包裹着当前的词法作用域，而真正执行却在其他地方。

模块模式雏形：
```
var foo = function(){
    var something = "cool";
    function dosomething(){
        console.log(something);
    }
    return{
        dosomething: dosomething
    }
}
foo().dosomething();//"cool"
 ```
模块模式也利用了闭包。

总结： 当函数可以记住并访问所在的词法作用域，该函数在当前词法作用域之外执行，这时就产生了闭包。

# 第二部分

## 第一章 关于this

### 为什么要使用this：
 this提供了一种优雅的方式来隐式“传递”一个对象引用，因此可以将API设计的更加简洁并且复用。

### this是什么：
this并不是代表指向自身，也不是代表它的作用域，代表函数的拥有者其实也是不准确的。而是取决于函数的调用方式，也就是说，this是发生在运行时的绑定，this的绑定和函数声明的位置没有任何关系，而是取决于函数调用的位置（调用栈）。

当一个函数被调用时，会创建一个活动记录（即执行上下文）。这个记录包含函数在哪里被调用（调用栈），调用方式，传入的参数等信息，this就是这个上下文的一个属性。

## 第二章 this全面解析

调用栈（调用位置）：就是一个函数A调用B,B调用C，则C函数的上下文记录的调用栈是A->B->C。

判断调用栈的意义在于，可以结合this绑定规则分析出this具体的指向含义。

### 绑定规则：

1. 默认绑定
函数在全局下直接调用，this指向全局对象（函数运行的内部必须处于非严格模式，而调用处是否严格模式则不受影响）。
严格模式下：this指向undefined。
2. 隐式绑定
函数作为对象的属性（最近的拥有对象）调用。this指向当前对象。
    1. 隐式丢失（解释了为什么回调里this对象不是我们想象中的那样）：
    ```
	function foo(){
		console.log(this.a);
	}
	var obj = {
		a: 2,
		foo: foo
	}
	var a = "oops,global";
	//因为函数名的传递赋值本质上是值传递（传递的是函数表达式），而和谁”拥有“调用的函数并没有任何关系。
	//所以此处赋值相当于 bar = function(){console.log(this.a)}。变成了默认绑定。
	var bar = obj.foo;
	bar() //"oops,global"
	function foo(){
		console.log(this.a);
	}
	function doFoo(fn) {
		//fn = foo
		fn();
	}
	var obj = {
		a: 2,
		foo: foo
	}
	var a = "oops,global";
	doFoo(obj.foo) //"oops,global"
	function foo(){
		console.log(this.a);
	}
	var obj = {
		a: 2,
		foo: foo
	}
	var a = "oops,global";
	setTimeout(obj.foo,100) //"oops,global"
        ```
在传回调函数的时候，回调函数本质上只是值传递，所以就相当于在传入的当前函数的作用域内重新定义了一个函数然后执行而已，这就导致了this并不是我们想象中的外部this了。这就是隐式丢失。所以才会在我们在一开始传入异步回调之前先进行类似于 var self = this；的赋值操作，然后在回调里使用self 替代this。
当然，有些第三方库会强制将回调的this指向进行修改，因为内部能很随意的进行修改函数的调用栈。比如jquery库中将this强制绑定在触发事件的DOM对象上。
传入回调的时候，我们完全没法控制this的指向，即无法明知它的调用栈。此时可以使用显示绑定。

3. 显示绑定
使用call、apply方法。
call(obj,arguments)，当obj传入一些基本数据类型如string，int，boolean，则会使用装箱机制转化为相应的对象new String(),new Boolean(), new Number()。
    1. 硬绑定<br>
        常见的使用场景是使用一个包裹函数里调用call，以此来解决隐式丢失的问题：
        ```
        function foo(b){
            console.log(this.a + b);
        }
        var obj = {
            a: 2
        }
        function bar(fn) {
            return foo.apply(obj,arguments);
        }
        1bar(3) //5

        可以创建一个辅助函数bind：
        function bind(fn,obj){
            return function(){
                return fn.apply(obj,arguments);
            }
        }
        var bar = bind(foo, obj);
        bar(3);//5
        ```
        因为这个模式很常用，所以ES5提供了内置的Function.prototype.bind方法。

    2. 手动传入"上下文"
    很多第三方库、js语言本身、宿主环境提供了许多新的内置函数，这些函数会提供一个可选的参数，指定该函数的上下文。内部其实就是通过call、apply实现的显示绑定。

    硬绑定是显示绑定的一种应用的叫法。显示绑定包括硬绑定。

4.  new绑定
js的构造函数：仅仅是一些在使用new操作符时被调用的普通函数而已。
所有的函数（包括内置对象函数）都可以使用new来调用，这种函数调用被称为构造函数调用。严格来说，并不存在什么构造函数，只有对于函数的构造调用。
函数new调用时会自动执行以下操作：
    1. 创建一个全新的对象。
    2. 新对象会被执行Prototype连接。
    3. 新对象会被绑定到构造的this上。
    4. 如果构造函数没有返回其他对象，则该构造函数调用会自动默认返回这个新对象。

5. 优先级，以此进行判断this的指向
new 绑定 > 显示绑定 > 隐式绑定 > 默认绑定

new绑定和硬绑定的一个柯里化应用:
通过bind预先传入函数的一些参数，在new时可以只传入剩下的参数值。
```
function foo(p1,p2){
    this.val = p1 + p2;
}
```

```
//传入null说明我们并不关心this是什么，因为设定也抢不过new。。。
var bar = foo.bind(null, "p1");
var baz = new bar("p2");
baz.val; //p1p2
```
在bind时候传入null可能会有副作用：如果某个函数确实使用了this，那默认规则会把this绑定到全局对象上，造成灾难。
所以应该传入Object.create(null)，这是js种创建一个空对象的最有效最安全的办法，因为它比{}更空（{}会创建prototype委托）

### ES6胖箭头 =>
箭头函数不使用this的四种规则，而是根据外层function或全局作用域决定this。
```
function foo(p1,p2){
    //返回一个箭头函数
    return (a) => {
        //this 是foo函数的this
        console.log(this.a);
    }
}
var obj1 = {
    a: 2
}
var obj2 = {
    a: 3
}
var bar = foo.call(obj1);
bar.call(obj2);//2
```
建议：
this风格有两种，任何时候都应该只使用其中一种。否则会带来代码混乱。
1. 完全采用this风格，使用bind，apply等。
2. 使用词法作用域，使用类似于self = this以及箭头函数。

## 第五章 原型

prototype属性只有函数拥有,函数默认具有这个公有但不可枚举的prototype属性，对象并没有。对象拥有的是内部[[prototype]]属性（私有属性，不对外公开。很多浏览器叫做\_\_proto\_\_属性）。

函数的prototype属性指向一个普通对象，该对象叫prototype对象（默认是一个普通的空对象{}而已）

### 属性设置与屏蔽：

在对对象进行赋值操作时，会触发[[ Get ]]操作,进行以下过程：
1. 检查对象本身是否具有该属性,有就直接返回；
2. 若没有，就会访问对象的原型链，此时就会涉及到属性设置与屏蔽问题。

在执行 myObj.foo = "bar"时候，若foo属性不存在于myObj对象上而是存在于原型链上，则会出现下面三种情况：
1. 该属性没有被设置为只读（writable: false），则会在myObj对象上添加foo属性，此时即发生属性屏蔽；
2. 该属性并被设置为只读，则该赋值语句被忽略。严格模式下报错。
3. 该属性被设置了setter，那么会一定调用该setter，属性不会添加到myObj。

若想忽略第二、三种情况，直属性，则不能使用=，而是使用Object.defineProperty()方法添加foo属性。

有些情况要小心，避免发生隐式屏蔽：
```
var anotherObject = {
    a:2
}
var myObject = Object.create(anotherObject);
anotherObject.a //2
myObject.a //2
anotherObject.hasOwnProperty("a"); //true
myObject.hasOwnProperty("a"); //false
myObject.a++; //隐式屏蔽！原因 => myObject.a = myObject.a + 1,等式右边读取原型对象的属性，赋值给左边则会发生屏蔽
anotherObject.a; //2
myObject.a; //3
myObject.hasOwnProperty("a") //true
```
hasOwnProperty()的作用：判断对象本身是否具有相应的属性而不是原型链上。
### 对象、类、函数、原型继承、constructor属性的关系

首先，js语言中，没有类的概念。很多时候都是一些开发者联想出来的。而原型继承也和类继承是正好相反的过程。原型继承通过关联实现，而类继承通过属性和方法复制达到。
js的原型继承，并不是实现对象的属性和方法的复制（类继承），而是通过原型的相互关联（即原型链）来层层代理，这样一个对象就可以通过委托来访问另一个对象的属性和方法，所以才会出现方法在原型链上的查找过程。
```
function Foo(a){
    console.log("Foo");
    this.a = a;
}
var foo = new Foo(2) // Foo ，new绑定this并执行Foo()函数并返回一个对象， {a: 2}
console.log(foo.a); //2
```
new Foo()是函数调用的一种形式（new调用，或者说叫构造函数调用（js中对于构造函数的定义是：所有带new的函数调用），此时Foo函数也会被称为构造函数。约定函数名首字母大写）。这种调用的作用不仅仅是实际执行一下Foo方法，它还会创建一个对象。该对象的内部[[prototype]]属性（可以使用Object.getPrototypeOf拿到该私有属性）会和Foo()函数的prototype属性指向的对象进行关联（注意，这里的关联会天生有代理功能，而且并不是赋值性的操作。实现js的继承机制其实就靠这玩意！！！），所以得出：
```
Object.getPrototypeOf(foo) === foo.__proto__ === Foo.prototype (该等式天生成立)
 ```
代理的功能： foo的属性和方法若找不到，就会到Foo.prototype这个对象中去寻找。

函数的原型对象有个属性叫constructor,这个属性返回的是构造函数自身，即：
```
Foo.prototype.constructor === Foo (该等式也天生成立)
```
特别能迷惑人的一点是： 为何以下等式也成立？
```
foo.constructor === Foo
```
并不是代表foo对象的constructor属性返回构造函数(foo作为一个普通对象，本身并没有constructor属性)。而是foo.constructor发生了委托（或者说代理），实际上访问的是Foo.prototype.constructor（找不到该属性就去原型对象上去找了）。
constructor 属性本身也是可写的，即可以自己改变该属性的返回值。constructor并不代表被构造，该属性非常不可靠。(tip: Foo.constructor === Function)

### 原型链：

对象a（A函数new出的对象）的内部[[prototype]]属性和A函数的prototype属性对象关联，A函数的prototype属性对象的内部[[prototype]]属性和B函数的prototype属性对象关联，B函数的prototype属性对象的内部[[prototype]]属性和C函数的prototype属性对象关联,C函数的prototype属性对象的内部[[prototype]]属性和D函数的prototype属性对象关联...
```
       a.__proto__   ===   A.p  => B.p
                                      A.p.__proto__  ===  B.p   =>  C.p                                   
                                                                       B.p.__proto__  ===   C.p     
                                                                                                          ... =>  Object.p
                                                                                                                    Object.p.__proto__ === null

注： => 代表关联，而不是引用； X.p 代表 X函数的prototype属性
即：A.p => B.p => C.p ，这就是原型链，就是代表A.prototype、B.prototype和C.prototype进行了关联（通过X.prototype.__proto__属性赋值）。原型链单单指prototype对象之间的关联，和__proto__没有关系。

```
```
以下等式都成立：
a.__proto__.__proto.__proto__ === C.p  （这不是原型链，只是getPrototypeOf方法的持续调用）
A.prototype.__proto__.__proto__ === C.p    
B.prototype.__proto__ === C.p
```
原型链的顶端是Object.prototype，所有普通对象都和内置的Object.prototype关联。注意，这里的Object是内置对象，Object本身又是object对象的构造函数，即Object指的既是内置对象，又是构造函数，其他内置对象也都类似。

最常用的关联方法(new函数调用)：
```
B.prototype = new C();
```
ES5通过以下方法实现这样的关联（Object.create）（es5之前需要这个方法的polyfill代码）：
```
B.prototype = Object.create(C.prototype)

//创建一个新对象，该对象的__proto__指向C.prototype，
//然后修改B.prototype引用指向这个新对象完成B.prototype对象替换
//不建议直接修改B.prototype.__proto__属性
//tip: Object.create(null)
//会创建一个拥有空[[prototype]]链接的对象，也就是没有原型链。这种对象叫“字典”，非常适合用来存储数据
```
ES6可以通过以下方法实现(Object.setPrototypeOf)：
```
Object.setPrototypeOf（B.prototype,C.prototype）
//直接让B.prototype对象和C.prototype进行关联
```
### 判断原型链之间的关系

1. 对象与函数之间的判断(instanceof)：
```
a instanceof A //true  //判断a是不是A函数的实例（a.__proto__ === A.prototype）
```
2. 对象与对象之间的判断(isPrototypeOf)：
```
B.prototype.isPrototypeOf(a)//true  //判断在 a 的整个原型链中，是否含有 B.prototype,也就是说B.prototype是否出现在a的原型链中,等价于b.isPrototypeOf(a)
```
注：
Object.prototype.isPrototypeOf(obj)
Object.getPrototypeOf(obj)：获取obj对象的上层函数的原型对象，即obj.\_\_proto\_\_
Object.setPrototypeOf(obj1,obj2)： 设置obj1对象关联委托到obj2对象

isPrototypeOf属于Object.prototype，所以所有的对象都可以访问该方法。
getPrototypeOf、setPrototypeOf属于Object内置对象
### \_\_proto\_\_

Object.prototype.\_\_proto\_\_       ： "笨蛋proto"
这代表\_\_proto\_\_并不是对象的自身属性，但是对象可以通过代理使用该属性。

该属性其实是一个getter/setter:
```
Object.defineProperty(Object.prototype,"__proto__",{
    get: function(){
        return Object.getPrototypeOf(this);
    },
    set: function(o) {
        Object.setPrototypeOf(this,o);
        return o;
    }
})
```
内部调用了Object.getPrototypeOf(obj)、Object.setPrototypeOf(obj1,obj2)

### 内部委托 > 直接委托

直接委托：
```
var anotherObject = {
    cool: function(){
         console.log("cool");
    }
}
var myObject = Object.create(anotherObject);
myObject.cool()//"cool"
```
当设计API的时候，如果myObject中不存在cool()方法却能“神奇”的运行时，会造成维护上的困难和理解上的障碍。需要通过内部委托来去除这种弊端，内部进行显式的this调用。设计api时不要直接暴露直接改用内部委托。

内部委托：
```
var anotherObject = {
    cool: function(){
        console.log("cool");
    }
}
var myObject = Object.create(anotherObject);
myObject.doCool = function(){
    this.cool()//内部委托
}
myObject.cool()//"cool"
```
这样看起来清晰很多。

## 第六章 行为委托

### 类理论

类设计模式鼓励： 在继承时使用方法重写（和多态），父类先将许多普遍行为抽象，然后子类根据自己的需求进行特殊化（重写）。
```
function Foo(who){
    this.me = who;
}
Foo.prototype.identify = function(){
    return "I am "+ this.me;
}
//Bar 继承 Foo，有两步
function Bar(who){
    Foo.call(this,who);//1.先将Foo上的变量进行转移
}
Bar.prototype = Object.create(Foo.prototype);//2.进行原型链接
Bar.prototype.speak = function () {
    alert("Hello," + this.identify() + '.');
}
var b1 = new Bar("b1");
var b2 = new Bar("b2");
b1.speak();
b2.speak();
```
### 委托理论

并没有类的父子关系，也没有继承概念，本质上只是方法的层层代理，各个对象有自己的方法，调用该对象不存在的方法时，就会通过代理委托寻找关联对象上的相应方法。
```
var Foo = {
   init: function(who){ this.me = who;}
   identify: function(){ return "I am " + this.me;}
}
var Bar = Object.create(Foo);
Bar.speak = function(ID,Label){
    alert("hello" + this.identify() + ".");
}
var b1 = Object.create(Bar);
var b2 = Object.create(Bar);
b1.init("b1");
b2.init("b2");
b1.speak();
b2.speak();
```
这个设计模式提倡：
1. 要将状态（变量）放置在对象obj1...上，不要放在Task对象上，因为Task的状态会被多个子对象共同修改。
2. 和类设计模式相反，委托模式尽量少使用容易被重新使用的方法名，提倡使用更有描述性的方法名。
3. 之前提过，在API的设计中，委托最好在内部实现，不要直接暴露出去，上面的speak方法。

这个模式不需要复杂和让人困惑的模仿类的行为（构造函数、原型和new）。

###  ES6 Class

class机制并不是真正意义上的类，本质上只是原型的语法糖。目的是避免显式的使用prototype。
class的好处：
1. 不再需要引用杂乱的prototype。
2. 通过extends，可以很自然的扩展对象类型，甚至是内置的对象类型。不再需要Object.create()，或Object.setPrototypeOf()。
3. 通过super()，实现相对多态，这样任何方法都可以引用原型链上层的同名方法。
4. Class不允许声明属性，只能声明方法，避免了很多共享属性问题。

坏处：
class加深了过去20多年对于JavaScript中“类”的误解。让本来优雅的[[prototype]]机制变得非常别扭.

### 鸭子类型：
比如验证某个对象是不是想要的对象，通过验证该对象是不是有相应的方法，如promise的then方法，判别该对象。会造成脆弱的设计，带来潜在的风险。ES6的promise就是典型的“鸭子类型”
