## 一 Redux简介

Redux 是 JavaScript 状态容器，提供可预测化的状态管理


###动机与目的
 JavaScript 单页应用开发日趋复杂，JavaScript 需要管理比任何时候都要多的 state （状态）。
 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等
 管理不断变化的 state 非常困难。state 在什么时候，由于什么原因，如何变化已然不受控制。

 一些库如 React 试图在视图层禁止异步和直接操作 DOM 来解决这个问题。
 美中不足的是，React 依旧把**处理 state 中数据的问题**留给了你。Redux就是为了解决这个问题。

 跟随 Flux、CQRS 和 Event Sourcing 的脚步，**通过限制更新发生的时间和方式**，
 Redux 试图**让 state 的变化变得可预测**。这些限制条件反映在 Redux 的 三大原则中.

 **Redux三大原则:**
 (1)**单一数据源**:整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中。
 (2)**State 是只读的,惟一改变 state 的方法就是触发 action**:action 是一个用于描述已发生事件的普通对象。视图和网络请求都不能直接修改 state，它们只能表达想要修改的意图。所有的修改都被集中化处理，且严格按照一个接一个的顺序执行,因此不用担心 race condition 的出现。 Action 是普通对象,可以被日志打印,后期调试或测试时回放出来。
 (3)**使用纯函数reducers来执行修改**：为了描述 action 如何改变 state tree ，需要编写 reducers,reducer 只是一些纯函数，它接收先前的 state 和 action，并返回新的 state。刚开始可以只有一个 reducer，随着应用变大，可以拆成多个小的 reducers，分别独立地操作 state tree 的不同部分,甚至编写可复用的 reducer 来处理一些通用任务，如分页器。

###优势：
可以让你构建一致化的应用，运行于不同的环境（客户端、服务器、原生应用）
简单清量（只有2kB）且没有任何依赖
由 Flux 演变而来，但受 Elm 的启发，避开了 Flux 的复杂性
做复杂应用和庞大系统时优秀的扩展能力。
可以用 action 追溯应用的每一次修改 (因此才有强大的开发工具。如录制用户会话并回放所有 action 来重现它)
单一的state tree:让同构应用开发变得非常容易。来自服务端的 state 可以在无需编写更多代码的情况下被序列化并注入到客户端中。调试也变得非常容易。

###和Flux的比较

**同：**
和 Flux 一样，Redux 将模型的更新逻辑集中于一个特定的层（Flux 里的 store，Redux 里的 reducer）。
Flux 和 Redux 都不允许程序直接修改数据，而是用一个叫作 “action” 的普通对象来对更改进行描述。

**异：**
1.Redux 没有 Dispatcher ,且不支持多个 store。
相反，只有一个单一的 store 和一个根级的 reduce 函数（reducer）。
随着应用不断变大，应该把根级的 reducer 拆成多个小的 reducers，
分别独立地操作 state 树的不同部分，而不是添加新的 stores。
这就像一个 React 应用只有一个根级的组件，这个根组件又由很多小组件构成。


## 二 Redux安装

安装稳定版：

npm install --save redux

多数情况下，还需要使用[React 绑定Redux的库](https://github.com/reactjs/react-redux)和[开发者工具](https://github.com/gaearon/redux-devtools)

npm install --save react-redux
npm install --save-dev redux-devtools

## 三 Redux技术要点

应用中所有的 state 都以一个对象树的形式储存在一个单一的 store 中。

惟一改变 state 的办法是触发 action，一个描述发生什么的对象。

为了描述 action 如何改变 state 树，你需要编写 reducers。

一个简单的例子：
```javascript
import { createStore } from 'redux';
/**
 * 这是一个 reducer，形式为 (state, action) => state 的纯函数。
 * 描述 action 如何把 state 转变成下一个 state。
 *
 * state 的形式可以是基本类型、数组、对象等数据结构。惟一的要点是：
 * 当 state 变化时需要返回全新的对象，而不是修改传入的参数。
 *
 * 下面例子使用 `switch` 语句和字符串来做判断，但你可以写帮助类(helper)
 * 根据不同的约定（如方法映射）来判断，只要适用你的项目即可。
 */
function counter(state = 0, action) {
  switch (action.type) {
  case 'INCREMENT':
    return state + 1;
  case 'DECREMENT':
    return state - 1;
  default:
    return state;
  }
}

// 创建 Redux store 来存放应用的状态
// API 是 { subscribe, dispatch, getState }
let store = createStore(counter);

// 可以手动订阅更新，也可以事件绑定到视图层
store.subscribe(() =>
  console.log(store.getState())
);

// 改变内部 state 惟一方法是 dispatch 一个 action
// action 可以被序列化，用日记记录和储存下来，后期还可以以回放的方式执行
store.dispatch({ type: 'INCREMENT' });
// 1
store.dispatch({ type: 'INCREMENT' });
// 2
store.dispatch({ type: 'DECREMENT' });
// 1
```


要做的修改变成一个普通对象，这个对象被叫做 action，而不是直接修改 state。
然后编写专门的函数决定每个 action 如何改变应用的 state，这个函数被叫做 reducer。


##四 Action

首先，要定义Action:

```javascript
/*
 * action 类型
 */

export const ADD_TODO = 'ADD_TODO';
export const TOGGLE_TODO = 'TOGGLE_TODO'
export const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER'

/*
 * 其它的常量
 */

export const VisibilityFilters = {
  SHOW_ALL: 'SHOW_ALL',
  SHOW_COMPLETED: 'SHOW_COMPLETED',
  SHOW_ACTIVE: 'SHOW_ACTIVE'
}

/*
 * action 创建函数
 */

export function addTodo(text) {
  return { type: ADD_TODO, text }
}

export function toggleTodo(index) {
  return { type: TOGGLE_TODO, index }
}

export function setVisibilityFilter(filter) {
  return { type: SET_VISIBILITY_FILTER, filter }
}
```


##五 Reducer

接下来创建Reducer:

**Action 只是描述了有事情发生了**这一事实，并没有指明**应用如何更新 state**。而这正是 reducer 要做的事情。

先设计 State 结构

在 Redux 应用中，所有的 **state 都被保存在一个单一对象**中。建议在写代码前先想一下这个对象的结构。如何才能以最简的形式把应用的 state 用对象描述出来。

###Reducer实质
reducer 就是一个纯函数，接收旧的 state 和 action，返回新的 state。
```javascript
(previousState, action) => newState
```

###处理 Reducer 关系时的注意事项：

通常，state 树还需要存放其它一些数据，以及一些 UI 相关的 state,尽量把这些数据与 UI 相关的 state 分开。
建议你尽可能地把 state 范式化，不存在嵌套。把所有数据放到一个对象里，每个数据以 ID 为主键，不同实体或列表间通过 ID 相互引用数据。把应用的 state 想像成数据库。
永远不要在 reducer 里做这些操作：修改传入参数；执行有副作用的操作，如 API 请求和路由跳转；调用非纯函数，如 Date.now() 或 Math.random()。
reducer 一定要保持纯净。只要传入参数相同，返回计算得到的下一个 state 就一定相同。没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算。

###初始化state
Redux 首次执行时，state 为 undefined，可先设置并返回应用的初始 state。

如：
```javascript
import { VisibilityFilters } from './actions'

const initialState = {
  visibilityFilter: VisibilityFilters.SHOW_ALL,
  todos: []
};

function todoApp(state, action) {
  if (typeof state === 'undefined') {
    return initialState
  }

  // 这里暂不处理任何 action，
  // 仅返回传入的 state。
  return state
}
```
###处理 SET_VISIBILITY_FILTER。

例如上面的例子需要做的可以是改变 state 中的 visibilityFilter：

```javascript
function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    default:
      return state
  }
}
```
注意：不要修改 state，可以使用 Object.assign() 新建了一个副本；在 default 情况下返回旧的 state。遇到未知的 action 时，一定要返回旧的 state。

###处理多个 action
一般写在switch语句中。

###拆分 Reducer

有时Reducer的代码有些冗长，把部分需要的state传给特定的函数来将Reducer拆分。每个 reducer 只负责管理全局 state 中它负责的一部分。每个 reducer 的 state 参数都不同，分别对应它管理的那部分 state 数据。也就是所谓的 reducer 合成，它是开发 Redux 应用最基础的模式。

随着应用的膨胀，我们还可以将拆分后的 reducer 放到不同的文件中, 以保持其独立性并用于专门处理不同的数据域。

Redux 提供了 combineReducers() 工具类，生成一个函数，这个函数来调用你的一系列 reducer，每个 reducer 根据它们的 key 来筛选出 state 中的一部分数据并处理，然后这个生成的函数再将所有 reducer 的结果合并成一个大的对象。

combineReducers 接收一个对象，可以把所有顶级的 reducer 放到一个独立的文件中，通过 export 暴露出每个 reducer 函数，然后使用 import * as reducers 得到一个以它们名字作为 key 的 object，如：

```javascript
import { combineReducers } from 'redux'
import * as reducers from './reducers'

const todoApp = combineReducers(reducers)
```

#六 Store

前面我们使用了action 来描述“发生了什么”，用 reducers 来根据 action 更新 state 。
而Store 就是把它们联系到一起的对象。

###Store 有以下职责：

维持应用的 state；
提供 getState() 方法获取 state；
提供 dispatch(action) 方法更新 state；
通过 subscribe(listener) 注册监听器;
通过 subscribe(listener) 返回的函数注销监听器。

Redux 应用只有一个单一的 store。当需要拆分数据处理逻辑时，你应该使用 reducer 组合 而不是创建多个 store。

###根据reducer创建store:
根据已有的 reducer 来创建 store 是非常容易的。前面使用 combineReducers() 将多个 reducer 合并成为一个。现在只需将其导入，并传递 createStore()。

```javascript
import { createStore } from 'redux'
import todoApp from './reducers'
let store = createStore(todoApp)
```

createStore() 的第二个参数是可选的, 用于设置 state 初始状态。这对开发同构应用时非常有用，服务器端 redux 应用的 state 结构可以与客户端保持一致, 那么客户端可以将从网络接收到的服务端 state 直接用于本地数据初始化。

```javascript
let store = createStore(todoApp, window.STATE_FROM_SERVER)
```

###发起 Actions

创建好 store ，即使还没有界面，已经可以测试数据处理逻辑了。

```javascript
import { addTodo, toggleTodo, setVisibilityFilter, VisibilityFilters } from './actions'

// 打印初始状态
console.log(store.getState())

// 每次 state 更新时，打印日志
// 注意 subscribe() 返回一个函数用来注销监听器
let unsubscribe = store.subscribe(() =>
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

可以在控制台看到 store 里的 state 是如何变化的：

在还没有开发界面的时候，就可以定义程序的行为。而且这时候已经可以写 reducer 和 action创建函数的测试。不需要模拟任何东西，因为它们都是纯函数。只需调用一下，对返回值做断言，写测试就是这么简单。


#七 Redux数据流

**严格的单向数据流**是 Redux 架构的设计核心。

这意味着应用中所有的数据都遵循相同的生命周期，这样可以让应用变得更加可预测且容易理解。同时也鼓励做数据范式化，这样可以避免使用多个且独立的无法相互引用的重复数据。

##Redux 应用中数据的生命周期遵循下面 4 个步骤：

###1.调用 store.dispatch(action)

Action 就是一个描述“发生了什么”的普通对象。比如：

```javascript
 { type: 'LIKE_ARTICLE', articleId: 42 };
 { type: 'FETCH_USER_SUCCESS', response: { id: 3, name: 'Mary' } };
 { type: 'ADD_TODO', text: 'Read the Redux docs.'};
 ```
 
可以把 action 理解成新闻的摘要。如 “玛丽喜欢42号文章。” 或者 “任务列表里添加了'学习 Redux 文档'”。

可以在任何地方调用 store.dispatch(action)，包括组件中、XHR 回调中、甚至定时器中。

###2.Redux store 调用传入的 reducer 函数。

Store 会把两个参数传入 reducer： 当前的 state 树和 action。例如，在这个 todo 应用中，根 reducer 可能接收这样的数据：

```javascript
 // 当前应用的 state（todos 列表和选中的过滤器）
 let previousState = {
   visibleTodoFilter: 'SHOW_ALL',
   todos: [
     {
       text: 'Read the docs.',
       complete: false
     }
   ]
 }

 // 将要执行的 action（添加一个 todo）
 let action = {
   type: 'ADD_TODO',
   text: 'Understand the flow.'
 }

 // render 返回处理后的应用状态
 let nextState = todoApp(previousState, action);
 
 ```
 
注意 reducer 是纯函数。它仅仅用于计算下一个 state。它应该是完全可预测的：多次传入相同的输入必须产生相同的输出。它不应做有副作用的操作，如 API 调用或路由跳转。这些应该在 dispatch action 前发生。

###3.根 reducer 把多个子 reducer 输出合并成一个单一的 state 树。

根 reducer 的结构完全由你决定。Redux 原生提供combineReducers()辅助函数，来把根 reducer 拆分成多个函数，用于分别处理 state 树的一个分支。

下面演示 combineReducers() 如何使用。假如有两个 reducer：一个是 todo 列表，另一个是当前选择的过滤器设置：

```javascript
 function todos(state = [], action) {
   // 省略处理逻辑...
   return nextState;
 }

 function visibleTodoFilter(state = 'SHOW_ALL', action) {
   // 省略处理逻辑...
   return nextState;
 }

 let todoApp = combineReducers({
   todos,
   visibleTodoFilter
 })
 ```
 
当你触发 action 后，combineReducers 返回的 todoApp 会负责调用两个 reducer：
```javascript
 let nextTodos = todos(state.todos, action);
 let nextVisibleTodoFilter = visibleTodoFilter(state.visibleTodoFilter, action);
 ```
 
然后会把两个结果集合并成一个 state 树：
```javascript
 return {
   todos: nextTodos,
   visibleTodoFilter: nextVisibleTodoFilter
 };
 ```
 
虽然 combineReducers() 是一个很方便的辅助工具，你也可以选择不用；可以自行实现自己的根 reducer。

###4.Redux store 保存根 reducer 返回的完整 state 树。

这个新的树就是应用的下一个 state，所有订阅 store.subscribe(listener) 的监听器都将被调用；监听器里可以调用 store.getState() 获得当前 state。

现在，可以应用新的 state 来更新 UI。如果你使用了 React Redux 这类的绑定库，这时就应该调用 component.setState(newState) 来更新。




#八 Redux学习资源收集

1不错的Redux教程：https://github.com/react-guide/redux-tutorial-cn#redux-tutorial

2Redux开发工具：https://github.com/gaearon/redux-devtools 支持编辑后实时预览，可以很大的提高Redux开发效率
