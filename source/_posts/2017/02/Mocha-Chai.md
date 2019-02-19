---
title: Mocha+Chai
tags:
  - Mocha
  - Chai
categories:
  - 前端测试
date: 2017-02-19 17:50:46
---
### 测试框架Mocha

Mocha作为一个单元测试框架，会提供一个单独的命令“mocha”,所以全局安装。

实例：
```
// add.js
function add(x, y) {
    return x + y;
}
module.exports = add;

// add.test.js
// 通常，测试脚本与所要测试的源码脚本同名，但是后缀名为.test.js（表示测试）或者.spec.js（表示规格）。
var add = require('./add.js');
var expect = require('chai').expect;
describe('加法函数的测试', function() {
    it('1 加 1 应该等于 2', function() {
        expect(add(1, 1)).to.be.equal(2);//chai提供断言功能
    });
});
```

测试脚本里面应该包括一个或多个describe块，每个describe块应该包括一个或多个it块。

describe块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数。it块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"1 加 1 应该等于 2"），第二个参数是一个实际执行的函数，该函数里一般加入断言。

### 断言库 chai

Chai 提供三种接口：
* Should / Expect （BDD），
* Asset（TDD)

BDD  API： http://chaijs.com/api/bdd/

TDD  API ： http://chaijs.com/api/assert/

1. **Expect**

```
// 相等或不相等
expect(4 + 5).to.be.equal(9);
expect(4 + 5).to.be.not.equal(10);
expect(foo).to.be.deep.equal({ bar: 'baz' });

// 布尔值为true
expect('everthing').to.be.ok;
expect(false).to.not.be.ok;

// typeof
expect('test').to.be.a('string');
expect({ foo: 'bar' }).to.be.an('object');
expect(foo).to.be.an.instanceof(Foo);

// include
expect([1,2,3]).to.include(2);
expect('foobar').to.contain('foo');
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo');

// empty
expect([]).to.be.empty;
expect('').to.be.empty;
expect({}).to.be.empty;

// match
expect('foobar').to.match(/^foo/);
```
基本上，expect断言的写法都是一样的。头部是expect方法，尾部是断言方法，比如equal、a/an、ok、match等。两者之间使用to或to.be连接。
```
var expect = require('chai').expect //此处不是方法
var foo = 'bar'
var beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };
expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.length(3);
expect(beverages).to.have.property('tea').with.length(3);
```

2. **should**
```
var should = require('chai').should() //actually call the function
//import 'chai/should'; ES6 写法
var foo = 'bar'
var beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };
foo.should.be.a('string');
foo.should.equal('bar');
foo.should.have.length(3);
beverages.should.have.property('tea').with.length(3);
```
Should本质是扩展Object.prototype。而Expect是一个函数。

在使用下列helpers时，可以直接使用should.xx

* should.exist
* should.not.exist
* should.equal
* should.not.equal
* should.Throw
* should.not.Throw

```
var should = require('chai').should();
db.get(1234, function (err, doc) {
    should.not.exist(err);
    should.exist(doc);
    doc.should.be.an('object');
});
```

3. **Assert**

```
var assert = require('chai').assert
var foo = 'bar'
var beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };
assert.typeOf(foo, 'string'); // without optional message
assert.typeOf(foo, 'string', 'foo is a string'); // with optional message
assert.equal(foo, 'bar', 'foo equal `bar`');
assert.lengthOf(foo, 3, 'foo`s value has a length of 3');
assert.lengthOf(beverages.tea, 3, 'beverages has 3 types of tea');
```
---

### 详解mocha
```
1. mocha  //默认运行test目录下的直接子文件（即测试用例）
2. mocha filen1  file2 file3 //运行file1 file2 file3 的测试用例。
3. mocha --recursive //自动寻找并执行test子目录下面所有的测试用例，不管哪个层级
4. //支持shell和node通配符
5. mocha test/unit/\*.js //指定执行test/unit目录下面的所有js文件。shell通配符
6. mocha 'test/\*\*/\*.@(js|jsx)‘ //node通配符
7. //参数
8. mocha --watch //监视指定的测试脚本。只要测试脚本有变化，就会自动运行Mocha
9. mocha --bail //指定只要有一个测试用例没有通过，就停止执行后面的测试用例。这对持续集成很有用
```

#### 1. mochawesome生成漂亮的测试报告
```
1. $ npm install --save-dev mochawesome //注意不是全局安装
2. $ ../node_modules/.bin/mocha --reporter mochawesome
```
测试结果报告在mochaawesome-reports子目录生成

![](http://7xs8pt.com1.z0.glb.clouddn.com/mocha+chai.png)

#### 2. ES6测试
```
1. //ES6转码，需要安装Babel。
2. $ npm install babel-core babel-preset-es2015 --save-dev
```

在项目根目录下新建一个.babelrc配置文件
```
1. {
2.  "presets": [ "es2015" ]
3. }
```
使用--compilers参数指定测试脚本的转码器
```
1. $ ../node_modules/mocha/bin/mocha
 --compilers js:babel-core/register
 ```
--compilers参数后面紧跟一个用冒号分隔的字符串，冒号左边是文件的后缀名，右边是用来处理这一类文件的模块名。上面代码表示，运行测试之前，先用babel-core/register模块，处理一下.js文件。
#### 3. 异步测试

Mocha默认每个测试用例最多执行2000毫秒，如果到时没有得到结果，就报错。对于涉及异步操作的测试用例，这个时间往往是不够的，需要用-t或--timeout参数指定超时门槛。
```
1. it('测试应该5000毫秒后结束', function(done) {
2.  var x = true;
3.  var f = function() {
4.    x = false;
5.    expect(x).to.be.not.ok;
6.    done(); // 通知Mocha测试结束
7.  };
8.  setTimeout(f, 4000);
9. });
```
上面的测试用例，需要4000毫秒之后，才有运行结果。所以，需要用-t或--timeout参数，改变默认的超时设置。
```
1. $ mocha -t 5000 timeout.test.js //将测试的超时时限指定为5000毫秒
```
在测试异步用例时，必须要在回调里使用done（）通知Mocha执行结束，否则会一直等到超时报错。done作为测试回调的参数传入。
```
1. mocha -s 1000 timeout.test.js //指定高亮显示耗时超过1000毫秒的测试用例
```

Mocha内置对Promise的支持，允许直接返回Promise，等到它的状态改变，再执行断言，而不用显式调用done方法。
```
1. it('异步请求应该返回一个对象', function() {
2.  return fetch('https://api.github.com')
3.    .then(function(res) {
4.      return res.json();
5.    }).then(function(json) {
6.      expect(json).to.be.an('object');
7.    });
8. });
```
#### 4. 测试用例的钩子函数

Mocha在describe块之中，提供测试用例的四个钩子：before()、after()、beforeEach()和afterEach()。它们会在指定时间执行。
```
1. describe('hooks', function() {
2.  before(function() {
3.    // 在本区块的所有测试用例之前执行
4.  });
5.  after(function() {
6.    // 在本区块的所有测试用例之后执行
7.  });
8.  beforeEach(function() {
9.    // 在本区块的每个测试用例之前执行
10.  });
11.  afterEach(function() {
12.    // 在本区块的每个测试用例之后执行
13.  });
14.  // test cases
15. });
```
DEMO：
```
1. describe('异步 beforeEach 示例', function() {
2.  var foo = false;
3.  beforeEach(function(done) {
4.    setTimeout(function() {
5.      foo = true;
6.      done();
7.    }, 50);
8.  });
9.  it('全局变量异步修改应该成功', function() {
10.    expect(foo).to.be.equal(true);
11.  });
12. });
```
#### 5. 用例管理

大型项目有很多测试用例。有时，我们希望只运行其中的几个，这时可以用only和skip方法。describe块和it块都允许调用only方法，表示只运行某个测试套件或测试用例，在同一个文件或者同一个套件里的其他用例则不会执行

还有skip方法表示跳过指定的测试套件或测试用例。
```
1. it.only('1 加 1 应该等于 2', function() {只执行该用例
2.  expect(add(1, 1)).to.be.equal(2);
3. });
4. it('任何数加0应该等于自身', function() { //不会执行
5.  expect(add(1, 0)).to.be.equal(1);
6. });
1. it.skip('任何数加0应该等于自身', function() {//不会执行
2.  expect(add(1, 0)).to.be.equal(1);
3. });
```
---
注： 以上来源于阮一峰的网络日志：

 http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html
