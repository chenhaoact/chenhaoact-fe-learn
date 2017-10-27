# react-router 4.0实践

## 一 安装
进行网站（将会运行在浏览器环境中）构建，应安装react-router-dom。react-router-dom暴露出react-router中暴露的对象与方法，因此**只需要安装并引用react-router-dom即可（不需要再安装react-router）**。

注意：
React Router在4.0中拆分为三个包：react-router,react-router-dom和react-router-native。react-router提供核心的路由组件与函数。其余两个则提供运行环境（即浏览器与react-native）所需的特定组件。



```
npm install --save react-router-dom
```

## 二 基本配置
对于网页项目，存在`<BrowserRouter>`与`<HashRouter>`两种组件。当存在服务区来管理动态请求时，需要使用`<BrowserRouter>`组件，而`<HashRouter>`适用于静态网站。

`<BrowserRouter>`通过浏览器输入路由直接去访问不行（可以在应用内通过link等跳转访问），而`<HashRouter>`通过浏览器输入路由就能直接去访问。

这里选择`<HashRouter>`。

其他按照[React Router 4 简易入门](https://segmentfault.com/a/1190000010174260)中的介绍配置即可。


## 参考
[译] 关于 React Router 4 的一切
https://juejin.im/post/5995a2506fb9a0249975a1a4

React Router 4 简易入门
https://segmentfault.com/a/1190000010174260

React Router中文官网
http://reacttraining.cn/

React Router中文文档
http://reacttraining.cn/web/guides/quick-start

一些react router4的中文教程收集
http://hao.caibaojian.com/30989.html