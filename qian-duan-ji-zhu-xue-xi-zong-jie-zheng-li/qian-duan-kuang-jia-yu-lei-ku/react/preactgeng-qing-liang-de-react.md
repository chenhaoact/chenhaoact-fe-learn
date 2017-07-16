# Preact-更轻量的React

## 一 简介

集团目前整体上使用React技术栈进行前端开发，对于一些活动页面，移动端页面，我们可能需要使用一个更轻量的技术以获得更好的性能，而目前有一些不错的React式的轻量级实现方案，如：[preact](https://github.com/developit/preact/),[react-lite](https://github.com/Lucifier129/react-lite),[inferno](https://github.com/infernojs/inferno)等，能够在保留react核心方法与开发模式的同时，有效降低代码资源的大小，进而提升性能，这里学习了preact并进行总结，希望能为大家的开发带来一些新的选择。

### 1用途

#### （1）适用场景

基于react开发的大部分项目，都可以使用preact，特别是移动端页面。

### 2优缺点及对比

#### （1）优点

##### a.更接近于实质

Preact 实现了一个可能是最薄的一层虚拟 DOM。它将虚拟 DOM 与 DOM 本身区别开，注册真实的事件处理函数，很好地与其它库一起工作。

##### b.小体积,轻量

大多数 UI 框架相当大，在应用程序js代码中占比较高。Preact却足够小，你的业务代码，是应用程序中最大的部分。**preact本身的bundle在gzip压缩后大概只有3kb，比React小很多**。更少js代码的加载，解析和执行，可以有效的提升应用的性能与体验。

##### c.快速，高性能

Preact 是快速的，不仅因为他的体积，**一个更简单和可预测的 diff 实现**，使它成为最快的虚拟 DOM 框架之一。它也包含**额外的性能优化特性**，如：批量自定义更新，可选的异步渲染，DOM 回收和通过关连状态优化的事件处理等。

##### d.易于开发与生产

在不需要牺牲生产力的前提，preact包含了有一些额外而便捷的功能以使得开发更简单高效，如：

props, state 和 context 可以被传递给 render\(\)；  
**可使用标准的 HTML 属性**，如 class 和 for；  
可使用 React 开发工具等。

##### e.和React生态系统兼容

可以无缝使用 React 生态系统中可用的数千个组件。增加一个简单的兼容层 preact-compat 到绑定库中，甚至可以在系统中使用非常复杂的 React 组件。

##### f.可以很容易的和[PWA（渐进式 Web 应用程序）](https://developers.google.com/web/progressive-web-apps/)配合工作，提供更好的用户体验

PReact官方的脚手架[preact-cli](https://github.com/developit/preact-cli)可以直接快速的构建一个PReact的渐进式 Web 应用程序。使得页面在加载的 [5 秒内就进行交互](https://infrequently.org/2016/09/what-exactly-makes-something-a-progressive-web-app/)。

#### （2）缺点

##### a.一定的学习与引入成本

虽然preact比较简单，但也需要一定的时间去学习掌握与引入。

##### b.稳定性

React的稳定性已得到多个项目以及数十亿用户的验证，故建议新启的项目，特别是活动页，移动端页面可以使用preact,而原有的React项目，尤其是大型项目，在引入preact的时候需要进行足够的验证，测试以保证项目的稳定性。

##### c.react自身的不断优化

随着版本的迭代，react自身也在性能，开发模式上做了很多优化，如：最新的react重大更新版本react@16在加载时间上相比react@15减少了接近1/3，已经很接近preact。

##### d.弄清楚性能瓶颈到底是什么

**应用的加载速度慢真的是由于React框架过大吗？如果不是，那就没有必要去改用preact**。很多工程师往往为了优化而优化，而且结合自身背景只做自己分内的优化，却忘记优化的最终目的是什么。**花更多的时间去解决更关键的问题**，而不是花在各种使用替换方案和解决其兼容性上。

#### （3）PReact和React的对比

##### a. Preact 并未完全实现React的每个特性

Preact 本身没有去重新实现一遍 React。它们有一些不同之处。大部份的不同都很细微，且可以完全通过 [preact-compat](https://github.com/developit/preact-compat) 去掉。在轻量级的基础上，Preact尝试 100% 去实现 React 的接口。

Preact 没尝试去包括 React 的每一个特性，是因为它想保持 轻量而专注。如：[PropType](https://github.com/developit/proptypes) 验证，[Children](https://facebook.github.io/react/docs/react-api.html),Synthetic Events,Preact并不认为它们是React开发中必要的部分，故未去实现，但如果想去使用，则可以通过 [preact-compat](https://github.com/developit/preact-compat) 来完整支持。

##### b. 版本兼容与迭代

对于 Preact 和 [preact-compat](https://github.com/developit/preact-compat)， 版本兼容通过 current 和 previous 主要的 React 发布去衡量。**当新的特性被 React 团队公布的时候，若考虑到项目目标如果非常合理，它们可能会被添加到 Preact 的核心当中**。

## 二 基本概念与技术重点整理

### （2）组件生命周期

| 生命周期方法 | 什么时候被调用 |
| :--- | :--- |
| `componentWillMount` | 在一个组件被渲染到 DOM 之前 |
| `componentDidMount` | 在一个组件被渲染到 DOM 之后 |
| `componentWillUnmount` | 在一个组件在 DOM 中被清除之前 |
| `componentWillReceiveProps` | 在新的 props 被接受之前 |
| `shouldComponentUpdate` | 在`render()`之前. 若返回`false`，则跳过 render |
| `componentWillUpdate` | 在`render()`之前 |
| `componentDidUpdate` | 在`render()`之后 |

### （3）在React项目中把 React 替换成 Preact

两种方式：  
（1）安装 preact-compat  
（2）把 React 的入口替换为 preact，并解决代码冲突

具体参考：  
[用 Preact 替换 React    
](https://preactjs.com/guide/switching-to-preact)

### （5）和其他的技术结合来进一步提升和监控性能

虽然 Preact 很适用于 PWA，但它也可以与许多其他工具和技术一起使用以进一步提升和监控性能，如：

1. [**webpack的代码拆分按需加载**](https://webpack.github.io/docs/code-splitting.html) 来分解代码，以便**只发送用户页面需要的代码**。根据需要延迟加载其余部分可提高页面加载时间。

2. [**Service Worker 缓存**](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)允许**离线缓存应用程序中的静态和动态资源**，实现即时加载和重复访问时更快的交互性。使用[sw-precache](https://github.com/GoogleChrome/sw-precache#wrappers-and-starter-kits)或[offline-plugin](https://github.com/NekR/offline-plugin)完成此操作。

3. [**PRPL**](https://developers.google.com/web/fundamentals/performance/prpl-pattern/)鼓励**向浏览器预先推送或预加载资源**，从而加快后续页面的加载速度。它基于代码拆分和 SW 缓存。

4. [**Lighthouse**](https://github.com/GoogleChrome/lighthouse/)允许你**审计（监控）渐进式 Web 应用程序的性能和最佳实践**，因此你能知道你的应用程序的表现情况。



## 三 使用实践及案例

## 四 资源与参考

### 1 [官网](https://preactjs.com/)

### 2 [文档](https://preactjs.com/guide/getting-started)

### 3 [源码](https://github.com/developit/preact/)

### 4 教程

#### （1）已学习：

[Preact -- React的轻量解决方案    
](https://github.com/lcxfs1991/blog/issues/13)

[Why you shouldn\`t use Preact, Fast-React, etc. to replace React today](http://imweb.io/topic/5955bdcc690607610fe2e96e)

#### （2）学习中：

#### （3）待学习：

官方教程：

其他教程：

### 5工具与资源

[preact-cli    
](https://github.com/developit/preact-cli)快速构建preact项目的脚手架并结合了PWA技术

