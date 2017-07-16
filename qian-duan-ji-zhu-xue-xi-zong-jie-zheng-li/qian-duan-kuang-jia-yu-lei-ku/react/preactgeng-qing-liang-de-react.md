#Preact-更轻量的React

## 一 简介

集团目前整体上使用React技术栈进行前端开发，对于一些活动页面，移动端页面，我们可能需要使用一个更轻量的技术以获得更好的性能，而目前有一些不错的React的轻量级实现方案，如：[preact](https://github.com/developit/preact/),[react-lite](https://github.com/Lucifier129/react-lite)等，能够在保留react核心方法的同时，有效降低代码资源的大小，进而提升性能，这里学习了preact并进行总结，希望能为大家的开发带来一些新的选择。

### 1用途
####（1）适用场景
基于react开发的大部分项目，都可以使用preact。

### 2优缺点及对比
####（1）优点
##### a.更接近于实质
Preact 实现了一个可能是最薄的一层虚拟 DOM。它将虚拟 DOM 与 DOM 本身区别开，注册真实的事件处理函数，很好地与其它库一起工作。

##### b.小体积,轻量
大多数 UI 框架相当大，在应用程序js代码中占比较高。Preact却足够小，你的业务代码，是应用程序中最大的部分。更少js代码的加载，解析和执行，可以有效的提升应用的性能与体验。

##### c.快速，高性能
Preact 是快速的，不仅因为他的体积，**一个更简单和可预测的 diff 实现**，使它成为最快的虚拟 DOM 框架之一。它也包含**额外的性能优化特性**，如：批量自定义更新，可选的异步渲染，DOM 回收和通过关连状态优化的事件处理等。

##### d.即时生产
在不需要牺牲生产力的前提，preact包含了有一些额外而便捷的功能以使得开发更简单高效，如：

props, state 和 context 可以被传递给 render()；
**可使用标准的 HTML 属性**，如 class 和 for；
可使用 React 开发工具。

##### e.生态系统兼容
在不需要牺牲生产力的前提，preact包含了有一些额外而便捷的功能以使得开发更简单高效，如：

props, state 和 context 可以被传递给 render()；
**可使用标准的 HTML 属性**，如 class 和 for；
可使用 React 开发工具。













####（2）缺点


## 二 基本概念与技术重点整理


## 三 使用实践及案例


## 四 资源与参考

### 1官网

### 2文档

### 3源码

### 4教程
#### （1）已学习：
[Preact -- React的轻量解决方案
](https://github.com/lcxfs1991/blog/issues/13)

#### （2）学习中：



#### （3）待学习：
官方教程：

其他教程：


### 5工具与资源









React 的 3kb 轻量化方案，拥有同样的 ES6 API
https://preactjs.com/

源码
https://github.com/developit/preact/

preact-cli
https://github.com/developit/preact-cli


