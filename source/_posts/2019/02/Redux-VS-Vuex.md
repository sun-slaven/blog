---
title: Redux VS Vuex
tags:
  - 状态管理
categories:
  - React
date: 2019-02-27 23:35:21
---
目前这两种状态库都有使用过，但是概念上容易发生混淆，所以整体的整理和对比一下，便于记忆。同时巩固一下知识点。
# 为何需要状态库
先简单聊一下这个问题，这个问题是我作为面试官经常问的一个问题，但是很多面试者的答案都不能让人满意。很多人只是会说，为了更方便的进行组件间的状态共享。
这个时候我会补充问一句，如果使用状态提升（state hoisting）是不是也可以解决这个问题？很多人的回答是肯定的，然后自身就动摇了自己的理由。
的确，更方便的进行状态共享是使用状态库的一个好处，但是仅仅这个原因就能决定我们引入这个玩意？何况这个玩意本身流程繁琐，是降低开发效率的事情。
其实可以从这几个角度回答：
1. 纵向上避免深层次的组件props传递
2. 横向上，兄弟组件可以更好的共享部分状态，而不用状态提升导致可能污染父组件的state属性（很多人只是回答这个点）
3. state会有清晰的修改历史，可以进行版本回退、日志监控等额外功能。
4. 当项目越来越复杂、组件间联动越来越多，状态共享越来越频繁，相比于以上三点，牺牲一定的开发效率能带来更好的开发质量以及系统稳定性、可监测性是值得的。

# Redux
## 1. action
本质上只是一个简单的对象，用于描述**有什么事情发生了**。形如：
```js
{ type: 'ADD_TODO', text: 'Go to swimming pool' }
```
约定使用type属性标定动作


##### Action 创建函数
就是生成 action 的方法，便于action的快速创建和移植而已。
```js
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
```
## 2. reducer
为了把 action 和 state 串起来的一个函数，描述了**如何更新state**
```js
(previousState, action) => newState
```
接收state对象和action对象，经过处理返回新的state对象

reducer可以切割成一些小函数来更新部分的state，最后再使用一个大的reducer来调用这些小的reducer
```js
function todoApp(state = {}, action) {
  return {
    todos: todos(state.todos, action),
    visibilityFilter: visibilityFilter(state.visibilityFilter, action)
  };
}
```
之所以将这样的函数称之为reducer，是因为这种函数与被传入 Array.prototype.reduce(reducer, ?initialValue) 里的回调函数属于相同的类型

不要修改 previousState，始终返回新的state对象，保持 reducer 是**纯函数**，永远不要在 reducer 里做这些操作：
* 修改传入参数；
* 执行有副作用的操作，如 API 请求和路由跳转；
* 调用非纯函数，如 Date.now() 或 Math.random()

Redux 提供了 **combineReducers()** 工具类来做上面 todoApp 做的事情
```js
import { combineReducers } from 'redux'

const todoApp = combineReducers({
  visibilityFilter,
  todos
})
```

## 3. Store
**Redux 应用只有一个单一的 store**

Store 有以下职责：
* 维持应用的 state；
* 提供 getState() 方法获取 state；
* 提供 dispatch(action) 方法更新 state；
* 通过 subscribe(listener) 注册监听器;
* 通过 subscribe(listener) 返回的函数注销监听器。

##### 1.创建一个store
```js
import { createStore } from 'redux'
import todoApp from './reducers'
let store = createStore(todoApp)
```
var store = createStore(reducer，initialState);

createStore() 的第二个参数是可选的, 用于设置 state 初始状态

##### 2.如何使用这个store
```js
// 打印初始状态
console.log(store.getState())

// 每次 state 更新时，打印日志
// 注意 subscribe() 返回一个函数用来注销监听器
const unsubscribe = store.subscribe(() =>
  console.log(store.getState())
)

// 发起一系列 action
store.dispatch(addTodo('Learn about actions'))
store.dispatch(addTodo('Learn about reducers'))
store.dispatch(addTodo('Learn about store'))
store.dispatch(toggleTodo(0))
store.dispatch(toggleTodo(1))
store.dispatch(setVisibilityFilter(VisibilityFilters.SHOW_COMPLETED))

// 停止监听 state 更新
unsubscribe();
```

## 4.middleware
它提供的是位于 action 被发起之后，到达 reducer 之前的扩展点。你可以利用 Redux middleware 来进行日志记录、创建崩溃报告、调用异步接口或者路由等等。

## 5.执行过程
##### 1. 调用store.dispatch(action)
你可以在任何地方调用 store.dispatch(action)，包括组件中、XHR 回调中、甚至定时器中。

##### 2. store自动调用传入的 reducer 函数

##### 3. 根 reducer 把多个子reducer输出合并成一个单一的 state 树。

##### 4. store 保存根reducer返回的完整 state 树

# Vuex
以下是一个典型的vuex实例
```js
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
```
## 1.action
是一个可带副作用的function，方法内commit一个mutations。
Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象（注意不是store实例）

分发一个action：
store.dispatch('increment'， payload)
## 2.mutation
是一个纯函数。更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。

分发一个mutation：
store.commit('increment', payload)

注意Mutation 需遵守 Vue 的响应规则，属性是对象时，需要以新对象替换老对象

## 3.module
Vuex 允许我们将 store 分割成模块（module）,其实就是对state树按模块分割成小的state
```js
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态

```

## 4. 执行过程
##### 1. dispatch一个action
##### 2. action中commit一个mutation
##### 3. mutation中直接更改state

# 对比
* action的概念不同，redux中是一个对象，vuex中是一个可带副作用的函数，因此作用是不同的。
* redux中的概念更复杂，抽象程度更高。vuex更易于理解，对异步处理等成本上使用更简单。
* redux的reducer和vuex的mutation概念上对应，都是用于更新state，区别在于前者必须要求返回全新的state对象，后者是遵循vue响应式系统修改state对象
* 都遵循严格的单向数据流

# 总结
抛开react大树好乘凉的背景，vue有如今的地位无疑是花了开发者很多心血的，个人感觉尤雨溪的api设计更贴近人认为的使用思维一些（redux更像是人适应框架的约束），vuex的使用流程虽然本质和redux一致，但是给人的感觉上使用流程却更加自然顺畅，当然，这个api设计不是说就一定是好，总是有利有弊的，问题仅仅是在于利弊如何取舍带来的差异（从react hooks角度暴露出这样设计会存在一定问题，不过事情总是有发展局限性的）

参照：

[redux中文](https://www.redux.org.cn/docs/faq/CodeStructure.html)

[vuex官网](https://vuex.vuejs.org/zh/guide/state.html)