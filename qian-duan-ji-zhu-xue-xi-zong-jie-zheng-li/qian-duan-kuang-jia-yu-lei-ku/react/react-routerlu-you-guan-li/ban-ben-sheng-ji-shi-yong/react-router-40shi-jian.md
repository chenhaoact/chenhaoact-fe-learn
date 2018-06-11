# react-router 4.0实践

## 一 安装
进行网站（将会运行在浏览器环境中）构建，应安装react-router-dom。react-router-dom暴露出react-router中暴露的对象与方法，因此**只需要安装并引用react-router-dom即可（不需要再安装react-router）**。

注意：
React Router在4.0中拆分为三个包：react-router,react-router-dom和react-router-native。react-router提供核心的路由组件与函数。其余两个则提供运行环境（即浏览器与react-native）所需的特定组件。



```
npm install --save react-router-dom
```

## 二 基本配置

### BrowserRouter和HashRouter的区别

`<BrowserRouter>`通过浏览器输入路由直接去访问不行（可以在应用内通过link等跳转访问），而`<HashRouter>`通过浏览器输入路由就能直接去访问。

**HashRouter会在访问的时候加 /#/，BrowserRouter不会。**

对于在浏览器中运行的项目，我们可以选择 `<BrowserRouter>` 和 `<HashRouter>` 组件，`<BrowserRouter>` 应该用在服务器处理动态请求的项目中（知道如何处理任意的URI），`<HashRouter>` 用来处理静态页面（只能响应请求已知文件的请求）。

**通常来说更推荐使用 `<BrowserRouter>`，可是如果服务器只处理静态页面的请求，那么使用 `<HashRouter>` 也是一个足够的解决方案。**




其他按照[React Router 4 简易入门](https://segmentfault.com/a/1190000010174260)中的介绍配置即可。

### history对象
history对象包括了location等数据，通过this.props.history可以拿到。

#### 请求参数获取
可以直接从网址里通过?x=1方式传参，通过this.props.history.location.search获取到路径中的请求参数：



```
//访问 localhost:9666/d?x=1
console.log(this.props.history.location.search) //?x=1
```

**this.props.history.location的格式类似于window.location。**

此时通过window.location.search是取不到?x=1参数的，因为window.location是取的浏览器hash后面的参数（#后面的参数，react-router通过欺骗浏览器的hash来实现了路由的控制与切换）。


## 三 react-router 4 和 之前版本的不同

在 v3 的例子中有而在 v4 中没有的是，使用 {props.children} 来嵌套组件。这是因为在 v4 中，`<Route>` 组件在何处编写，如果路由匹配，子组件将在那里渲染。

具体参考：
[[译] 关于 React Router 4 的一切
](https://juejin.im/post/5995a2506fb9a0249975a1a4)





## 参考
[[译] 关于 React Router 4 的一切
](https://juejin.im/post/5995a2506fb9a0249975a1a4)

React Router 4 简易入门
https://segmentfault.com/a/1190000010174260

React Router中文官网
http://reacttraining.cn/

React Router中文文档
http://reacttraining.cn/web/guides/quick-start

一些react router4的中文教程收集
http://hao.caibaojian.com/30989.html