# Preact-更轻量的React

## 一 简介

集团目前整体上使用React技术栈进行前端开发，对于一些活动页面，移动端页面，我们可能需要使用一个更轻量的技术以获得更好的性能，而目前有一些不错的React式的轻量级实现方案，如：[preact](https://github.com/developit/preact/),[react-lite](https://github.com/Lucifier129/react-lite),[inferno](https://github.com/infernojs/inferno)等，能够在保留react核心方法与开发模式的同时，有效降低代码资源的大小，进而提升性能，这里学习了preact并进行总结，希望能为大家的开发带来一些新的选择。

### 1用途

#### （1）适用场景

基于react开发的大部分项目，都可以使用preact，特别是移动端页面（比如腾讯手机QQ就在不少场景下使用preact）。

### 2优缺点及对比

#### （1）优点

##### a.更接近于实质

Preact 实现了一个可能是最薄的一层虚拟 DOM。它将虚拟 DOM 与 DOM 本身区别开，注册真实的事件处理函数，很好地与其它库一起工作。

##### b.小体积,轻量

大多数 UI 框架相当大，在应用程序js代码中占比较高。Preact却足够小，你的业务代码，是应用程序中最大的部分。**preact本身的bundle在gzip压缩后大概只有3kb，比React小很多**。更少js代码的加载，解析和执行，可以有效的提升应用的性能与体验。

##### c.快速，高性能

Preact 是快速的，不仅因为它的体积，**一个更简单和可预测的 diff 实现**，使它成为最快的虚拟 DOM 框架之一。它也包含**额外的性能优化特性**，如：批量自定义更新，可选的异步渲染，DOM 回收和通过关连状态优化的事件处理等。

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

##### a.稳定性

React的稳定性已得到多个项目以及数十亿用户的验证，故建议新启的项目，特别是活动页，移动端页面可以使用preact,而原有的React项目，尤其是大型项目，在引入preact的时候需要进行足够的验证，测试以保证项目的稳定性。

##### b.react自身的不断优化

随着版本的迭代，react自身也在性能，开发模式上做了很多优化，如：最新的react重大更新版本react@16在加载时间上相比react@15减少了接近1/3，已经很接近preact。

##### c.弄清楚性能瓶颈到底是什么

**应用的加载速度慢真的是由于React框架过大吗？如果不是，那就没有必要去改用preact**。很多工程师往往为了优化而优化，而且结合自身背景只做自己分内的优化，却忘记优化的最终目的是什么。**花更多的时间去解决更关键的问题**，而不是花在各种使用替换方案和解决其兼容性上。

#### （3）PReact和React的对比

##### a. Preact 并未完全实现React的每个特性

Preact 本身没有去重新实现一遍 React。它们有一些不同之处。大部份的不同都很细微，且可以完全通过 [preact-compat](https://github.com/developit/preact-compat) 去掉。在轻量级的基础上，Preact尝试 100% 去实现 React 的接口。

Preact 没尝试去包括 React 的每一个特性，是因为它想保持 轻量而专注。如：[PropType](https://github.com/developit/proptypes) 验证，[Children](https://facebook.github.io/react/docs/react-api.html),Synthetic Events,Preact并不认为它们是React开发中必要的部分，故未去实现，但如果想去使用，则可以通过 [preact-compat](https://github.com/developit/preact-compat) 来完整支持。

##### b. 版本兼容与迭代

对于 Preact 和 [preact-compat](https://github.com/developit/preact-compat)， 版本兼容通过 current 和 previous 主要的 React 发布去衡量。**当新的特性被 React 团队公布的时候，若考虑到项目目标如果非常合理，它们可能会被添加到 Preact 的核心当中**。

**Preact 实现的几个关键项目目标:**
性能：快速与高效的渲染
大小：小，轻 (大约 3.5kb)
效率：高效的内存使用 (对象重复利用, 避免垃圾回收)
可理解性：可以几小时理解框架代码
兼容性：Preact 兼容大部分的 React API。 preact-compat 实现了更多的 react api 兼容。

**符合项目目标的React特性才会被添加到PReact。**

## 二 基本概念与技术重点整理
### （1）组件
Preact 中有两种组件（和React类似）：

#### a. 传统的组件：（带有生命周期方法和状态）

```
class Link extends Component {
    render(props, state) {
        return <a href={props.href}>{ props.children }</a>;
    }
}

```

注意，这里就用到了**PReact可以直接在render中传入props和state**的特性，从一定程度上简化了写法，提升了可读性。

#### b. 无状态的函数式组件：本质上是接受 props 并返回 JSX 的函数

```
const Link = ({ children, ...props }) => (
    <a {...props}>{ children }</a>
);

```

这个组件没有 state（只传了state）－某些情况下，**我们希望传递相同的 props 来渲染组件，并得到相同的结果。无状态的函数式组件往往是最好的选择**。无状态的函数式组件只是一种函数，接受 props 参数并返回 JSX。

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


### （3）关联状态
在优化 state 改变的方面，Preact 比 React 走得更超前一点。在 ES2015 React 代码中，通常的模式是在 render() 方法中使用箭头函数，以便响应事件，更新状态。**每次渲染都再局部创建一个函数闭包，效率十分低下，而且会迫使垃圾回收器作许多不必要的工作。**

在 Preact 的 Form 中，提供了 linkState() 作为解决方案。linkState() 是 Component 类的一个内置方法。

当发生一个事件时，调用 .linkState('text') 将返回一个处理器函数，这个函数把它相关的值更新到组件状态内指定的值。 **多次调用 linkState(name)时，如果 name 参数相同，那么结果会被缓存起来**。所以就必然不存在**性能**问题，如:



```
class Foo extends Component {
    render({ }, { text }) {
        return <input value={text} onInput={this.linkState('text')} />;
    }
}

```

这里`input`框输入的值就能立刻变为text的值赋值给value属性。

这样写简介明了，易于理解且高效。它能处理来自任何输入形式的关联状态。 **可选的第二参数 'path' 能够提供一个路径（形如：foo.bar.baz）给新的状态，用于自定义绑定**（如绑定到第三方组件的值）。


### (4) 外部 DOM 修改

有时，需要用到一些第三方库，这些**第三方库需要能够自由的修改 DOM，并且在 DOM 内部持久化状态，或这些第三方库根本就没有组件化**。有许多优秀的 UI 工具或可复用的元素都是处于这种无组件化的状态。在 Preact 中 (React 中也类似), 使用这样的库需要告诉 Virtual DOM 的 rendering/diffing 算法：在给定的组件(或者该组件所呈现的 DOM) 中不要去撤销任何外部 DOM 的改变。

可以在组件中定义一个 shouldComponentUpdate() 方法并让其返回值为 fasle：

```

class Block extends Component {
  shouldComponentUpdate = () => false;
}
```

有了这个生命周期的钩子（shouldComponentUpdate），并**告诉 Preact 当 VDOM tree 发生状态改变的时候, 不要去再次渲染该组件**。这样**组件就有了一个自身的根 DOM** 元素的引用。你**可以把它当做一个静态组件**，直到被移除。因此，任何的组件引用都可以简单通过 this.base 被调用，并且对应从 render() 函数返回的根 JSX 元素。


### （7）在React项目中把 React 替换成 Preact

两种方式：  
（1）安装 preact-compat  
（2）把 React 的入口替换为 preact，并解决代码冲突

具体参考：  
[用 Preact 替换 React    
](https://preactjs.com/guide/switching-to-preact)

### （8）将PReact和其他的技术结合来进一步提升和监控性能

虽然 Preact 很适用于 PWA，但它也可以与许多其他工具和技术一起使用以进一步提升和监控性能，如：

1. [**webpack的代码拆分按需加载**](https://webpack.github.io/docs/code-splitting.html) 来分解代码，以便**只发送用户页面需要的代码**。根据需要延迟加载其余部分可提高页面加载时间。

2. [**Service Worker 缓存**](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)允许**离线缓存应用程序中的静态和动态资源**，实现即时加载和重复访问时更快的交互性。使用[sw-precache](https://github.com/GoogleChrome/sw-precache#wrappers-and-starter-kits)或[offline-plugin](https://github.com/NekR/offline-plugin)完成此操作。

3. [**PRPL**](https://developers.google.com/web/fundamentals/performance/prpl-pattern/)鼓励**向浏览器预先推送或预加载资源**，从而加快后续页面的加载速度。它基于代码拆分和 SW 缓存。

4. [**Lighthouse**](https://github.com/GoogleChrome/lighthouse/)允许你**审计（监控）渐进式 Web 应用程序的性能和最佳实践**，因此你能知道你的应用程序的表现情况。



## 三 使用实践及案例

这里使用[preact-cli](https://github.com/developit/preact-cli)快速构建一个结合了PWA技术的preact项目。



```
# 安装preact-cli
npm i -g preact-cli

# 创建一个preact应用
preact create my-first-preact-app
cd my-first-preact-app
```

### 启动开发环境


```
npm start

```

基本上10秒左右就会编译完成，打开 http://0.0.0.0:8080/
就可以看到页面，**第一次打开，不到1秒页面就会加载出来，性能非常不错**：


![](/assets/preact1@2x.png)


### 打包构建


```
npm run build
```

打包构建也很快（不到10秒），而且打包完的资源非常小：

![](/assets/preact2@2x.png)



### 开发

项目结构如下：
![](/assets/preact3@2x.png)

其实，和一个React项目一样，且开发方式也非常类似，有一定React基础的同学基本都可以很快上手，这里就不在赘述。**像一些移动端的页面以及活动页建议可以尝试一下，性能确实会比React好一些，开发与构建流程也很简单高效。**

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

[基于PReact的一些项目代码与demo
](https://preactjs.com/about/demos-examples)

[PReact的一些库和插件（React本身相关的库与插件除外）
](https://preactjs.com/about/libraries-addons)

[使用Enzyme来测试组件
](https://preactjs.com/guide/unit-testing-with-enzyme)