## 简介
dva 是基于现有应用架构 (redux + react-router + redux-saga 等)的一层轻量封装，没有引入任何新概念

除了 react 和 react-dom 是 peerDependencies 以外，dva 封装了所有其他依赖。

**最核心的是提供了 app.model 方法，用于把 reducer, initialState, action, saga 封装到一起**

### 优缺点
#### 优点
简单，好用，结构清晰

#### 缺点
个人项目，99%的代码来自一个开发者，存在一些不确定性。

react-router、react、redux 的版本每一次迭代都会对项目产生影响，dva内置的版本不一定和最新的版本一致，一旦自行升级，就相当于主动挖了一个坑，此时就要在使用 dva 和使用新版本的组件上做出选择。


## 参考

https://github.com/dvajs/dva

### 教程
dva 介绍
https://github.com/dvajs/dva/issues/1

Getting Started
https://github.com/dvajs/dva/blob/master/docs/GettingStarted.md

12 步 30 分钟，完成用户管理的 CURD 应用 (react+dva+antd) 
https://github.com/sorrycc/blog/issues/18



