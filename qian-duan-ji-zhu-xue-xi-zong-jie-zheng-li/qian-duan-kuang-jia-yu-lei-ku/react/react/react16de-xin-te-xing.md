# React 16 新特性

### render 函数可以返回 HTML 片段和字符串

### Portals：提供了一种非常好的方式将 children 呈现到存在于父组件的DOM层次结构之外的DOM节点


```
ReactDOM.createPortal(child, container)

```
### 更好的支持服务端渲染
React 16 中的服务器呈现速度大大高于 React 15 的 三倍
将尝试尽可能重用现有的DOM。没有更多的校验

为什么React 16 SSR比React 15快得多？ 在React 15中，服务器和客户端渲染路径或多或少是相同的代码。 这意味着维护虚拟DOM所需的数据结构都将在服务器呈现时进行设置，即使在对renderToString的调用返回时，vDOM也被丢弃。 这意味着在服务器渲染路径上有很多浪费的工作。

然而，在React 16中，核心团队从头开始重写了服务器渲染器，并且根本没有进行任何vDOM的工作。 这意味着它可以快得多。

react 16升级了很多react的性能，其中惹人注目的就是他的服务端性能是大幅度的提升

### 支持自定义 DOM 属性

React 可以将无法识别的 HTML 和 SVG 属性传递给 DOM，而不是忽略它们

### 基于 Fiber核心架构的第一个版本（Fiber 负责 React 16 中的大部分新功能，开始解锁 React 的全部潜力）
async rendering(异步渲染)是我们正在研究的最令人激动的领域 ---- 我们的策略是通过定期向浏览器执行协同调度渲染工作。 使用异步渲染后，我们发现，整个应用程序表现的更加灵敏，因为 React 解决了主线程阻塞的问题。

## 参考：
[译]React v16.0 正式发布
https://github.com/iuap-design/blog/issues/236
