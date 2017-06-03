# Rax学习总结

## 一 简介

### 1用途

`Rax`是一个**通用的跨容器的渲染引擎**， 如果你使用过`React`， 那么你就已经知道了该如何使用`Rax`

， 因为它们的 API 是完全兼容的。

**简单的说就是可以使用react的写法开发跨平台的移动端应用和h5页面。**

旨在Write Once, Run everywhere。

跨容器：

同时在浏览器、Weex、Node.js 中运行

高性能：

超快的虚拟 DOM

超轻量：

8.0 kb min+gzip 运行大小

丰富的组件

### 2优缺点及对比

## 二 基本概念

Rax 的 DSL 语法是基于 React JSX 语法而创造。与 React 不同，在 Rax 中 JSX 是必选的，它不支持通过其它方式创建组件，所以学习 JSX 是使用 Rax 的必要基础。



## 三 使用实践及案例

首先，按照下列链接rax开发环境并初始化一个rax项目：

[https://alibaba.github.io/rax/guide/getting-started](https://alibaba.github.io/rax/guide/getting-started)



终端中会显示两个二维码，其中第一个是 Web 页面地址，第二个是 Weex 页面地址。

（在浏览器环境直接扫描第一个二维码，可以得到 Web 页面；通过 Weex Playground App 扫描第二个二维码访问该地址，则会返回相应的 Native 页面）



默认页面的代码在public/index.html，js代码在src/App.js，语法使用react的jsx



## 四 资源

### 1官网

[https://alibaba.github.io/rax/](https://alibaba.github.io/rax/)

组件：

[https://alibaba.github.io/rax/component](https://alibaba.github.io/rax/component)

主题：

[https://alibaba.github.io/rax/theme/more](https://alibaba.github.io/rax/theme/more)

### 2文档

[https://alibaba.github.io/rax/guide](https://alibaba.github.io/rax/guide)

### 3源码

[https://github.com/alibaba/rax](https://github.com/alibaba/rax)

### 4教程

官方教程：

[https://alibaba.github.io/rax/guide/getting-started](https://alibaba.github.io/rax/guide/getting-started)

其他教程：

