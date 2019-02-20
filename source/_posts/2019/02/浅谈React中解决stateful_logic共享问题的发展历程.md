---
title: 浅谈React中解决stateful logic共享问题的发展历程
date: 2019-02-21 00:15:41
tags:
  - mixin
  - hoc
  - render props
  - hooks
categories:
  - React
---

前端组件化时代，不可避免的要让代码逻辑在组件间复用，由此产生了很多不同的解决方案，比如vue的mixin，react的方案比较多，本文主要讲述一下react的方案演变之路

# 1.Mixin
问题：
1. Mixin 引入了隐式依赖关系
随着项目复杂度提升，会演变成复杂的mixin依赖关系图，形成黑盒。而开发人员对某个mixin的修改很心惊胆战，一旦写入，mixin很难删除或更改。不好的想法不会被重构，因为重构风险太大
2. Mixins导致名称冲突
mixin的实现方式会引起同一个命名空间下名称冲突
3. 破坏封装性
随着时间推移，会导致使用mixin的组件封装边界逐渐消失，由于很难改变或移除现有的混合，他们不断变得抽象，直到没人理解它们是如何工作的
[推荐一篇讲的比较好的博文](https://lizhiyao.github.io/2018/01/05/mixins-considered-harmful/)

# 2.HOC
## 2.1 什么是hoc
主要有两种实现方式：属性代理（Props Proxy）与反向继承（Inheritance Inversion）
第一种实现方式：
```js
const PopupContainer = (Wrapper) =>
  class WrapperComponent extends Component {
    componentDidMount() {
      console.log('HOC did mount')
    }

    componentWillUnmount() {
      console.log('HOC will unmount')
    }

    render() {
      return <Wrapper {...this.props} />;
    }
  }
```
第二种实现方式：
```js
const PopupContainer = (Wrapper) =>
  class WrapperComponent extends Wrapper {
    static propTypes = Object.assign({}, Component.propTypes, {
      foo: React.PropTypes.string,
    });

    componentDidMount() {
      super.componentDidMount && super.componentDidMount();
      console.log('HOC did mount')
    }

    componentWillUnmount() {
      super.componentWillUnmount && super.componentWillUnmount();
      console.log('HOC will unmount')
    }
    render() {
        return super.render();
  }
```
使用hoc：
```js
class MyComponent extends Component {
  render() {}
}

export default PopupContainer(MyComponent);
```

反向继承允许高阶组件通过this关键词获取 WrappedComponent，意味着它可以获取到 state，props，组件生命周期（component lifecycle）钩子，以及渲染方法（render）
## 2.2 hoc的优缺点
问题：
1. 静态方法丢失
当使用高阶组件包裹原始组件，返回的新组件会丢失原始组件的所有静态方法
2. Refs属性不能传递

优势：
1. 代码复用，代码模块化
2. 渲染劫持, 操作state
3. Props 增删改

# 3. render props
render prop 是一个组件用来了解要渲染什么内容的**函数 prop**。注意这是一个模式，而不是说有个props叫render，该属性可以被叫做children或其他任何属性。因此以下写法其实就是一个render props。
```html
<Mouse children={mouse => (
  <p>The mouse position is {mouse.x}, {mouse.y}</p>
)}/>
```
当然也可以写成
```html
<Mouse>
  {mouse => (
    <p>The mouse position is {mouse.x}, {mouse.y}</p>
  )}
</Mouse>
```
这是Mouse组件的render方法:
```js
render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>
        {this.props.render(this.state)}
      </div>
    );
  }
```
特点
1. render props的fn可以获取props对应的组件的scope，提升了渲染内容的灵活性
2. 个人感觉无非就是一个简单属性的使用提取成一个模式，但是这种使用方法有点反向流，而且在大多数场景下不是很必要，可以使用state hosting来避免。

# 4. hooks
v16.8后提倡的一个理念，提倡使用hooks替代class声明写法

先说为什么引入hooks？（以下来源于官网）
1. 难以重用和共享组件中的与状态相关的逻辑
2. 逻辑复杂的组件难以开发与维护，当我们的组件需要处理多个互不相关的 local state 时，每个生命周期函数中可能会包含着各种互不相关的逻辑在里面。（其实就是生命周期钩子函数中充斥着各种side effect，这部分增加了测试与风险成本）
3. 类组件中的this增加学习成本，类组件在基于现有工具的优化上存在些许问题。
4. 由于业务变动，函数组件不得不改为类组件等等。

hooks的优势：
1. custom Hooks实现组件的逻辑复用，状态和相关的处理逻辑（stateful logic）可以按照功能进行划分，不必散落在各个生命周期中，大大降低了开发和维护的难度
2. hooks会让side effect可控，降低风险

# 总结
整体梳理了一下react在逻辑复用方向上的一个演变历程，从使用过vue的mixin经验来说，mixin给我带来的恐惧是巨大的，而且编写unit test也很麻烦。但是hoc和render props的使用方式并不能给开发体验和开发成本带来多少好处，更像是以编程手段让人服从代码的复杂性。hooks虽然也不是最终解决方案，但是无疑要比之前的方案更让人接受，优势更明显。

一个stateful logic的共享问题，能牵扯出这么多的知识和问题，真心想说，**前端真的能折腾啊！！！**
