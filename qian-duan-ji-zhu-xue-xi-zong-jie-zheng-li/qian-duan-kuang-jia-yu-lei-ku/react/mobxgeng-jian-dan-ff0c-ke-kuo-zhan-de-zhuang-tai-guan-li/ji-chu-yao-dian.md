# 基础要点
## 一 简介

### 作用
通过透明的函数响应式编程使得状态管理变得简单和可扩展。

设计理念：任何源自应用状态的东西都应该自动地获得。

React 和 MobX 和组合：React 通过提供机制把应用状态转换为可渲染组件树并对其进行渲染。而MobX提供机制来存储和更新应用状态供 React 使用。


### 特点
提供了**优化应用状态与 React 组件同步**的机制，这种机制使用**响应式虚拟依赖状态图表**，它**只有在真正需要的时候才更新状态并且永远保持是最新**的。

MobX 会对在执行跟踪函数期间读取的任何现有的可观察属性做出反应。

### MobX和Redux的对比


## 二 核心概念
### 1. Observable state(可观察的状态)  @observable 

MobX 为现有数据结构(如对象，数组和类实例)添加了可观察的功能。 通过使用 @observable 装饰器来给类属性添加注解就可完成。

**注意：并不是所有数据都需要加它进行实时观察的（该数据一变组件立即重新渲染），需要这样功能的数据项再加。**

```
class Todo {
    id = Math.random();
    @observable title = "";
}
```



使用 observable 很像把对象的属性变成excel的单元格。 但和单元格不同的是，这些值不只是原始值，还可以是引用值，比如对象和数组。 你甚至还可以自定义可观察数据源。

注意：
这些 **@ 开头的东西是ES.next装饰器**。 在 MobX 中使用它们完全是可选的。但是利用像装饰器这样的ES.next的特性是使用 MobX 的最佳选择。 

具体使用参见[装饰器文档](https://mobx.js.org/best/decorators.html)。 

#### 使用observer把react组件变响应式组件（数据变立即重新渲染对应部分）
如果用 React，可**把(无状态函数)组件变成响应式组件，需在组件上添加 observer 函数/ 装饰器（然后就可以配合@observable的变量数据使用了）**. observer由 mobx-react 包提供的:

```
import React, {Component} from 'react';
import ReactDOM from 'react-dom';
import {observer} from "mobx-react";

//方法一：上面加@observer
@observer
class TodoListView extends Component { ... }

//方法二：使用observer(）
const TodoView = observer(({todo}) =>
    <li>
        <input
            type="checkbox"
            checked={todo.finished}
            onClick={() => todo.finished = !todo.finished}
        />{todo.title}
    </li>
)

const store = new TodoList();
ReactDOM.render(<TodoListView todoList={store} />, document.getElementById('mount'));

```
observer 会将 React (函数)组件转换为它们需要渲染的数据的衍生。 当**使用 MobX 所有的组件都会以巧妙的方式进行渲染，而只需一种简单无脑的方式来定义它们**。**MobX 会确保组件总是在需要时重新渲染**，但仅此而已。

### 2. Computed values(计算值)  @computed

定义在**相关数据发生变化时自动更新的值**。 通过@computed 装饰器或者用 (extend)Observable 时调用 的getter / setter 函数来使用。



```
//当添加了一个新的todo或者某个todo的 finished 属性发生变化时，MobX 会确保 unfinishedTodoCount 自动更新
class TodoList {
    @observable todos = [];
    @computed get unfinishedTodoCount() {
        return this.todos.filter(todo => !todo.finished).length;
    }
}
```

这样的计算可以很好地与电子表格程序中的公式(如MS Excel)进行比较。每当只有在需要它们的时候，它们才会自动更新。

### 3. Reactions(反应)

Reactions 和计算值很像，但它**不是产生一个新的值，而是会产生一些副作用**，如打印到控制台、网络请求、递增地更新 React 组件树以修补DOM等。 简而言之，**reactions 在 响应式编程和命令式编程之间建立沟通的桥梁。**


### 4. Actions(动作)





