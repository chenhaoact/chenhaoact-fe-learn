# React重点整理

## 一 简介

### 1用途

创造 React 是为了解决一个问题：构建随着时间数据不断变化的大规模应用程序。

### 2优缺点及对比

#### （1）优点

简单。仅仅只要表达出应用程序在任一个时间点应该呈现的样子，当底层的数据变了，React会自动处理所有界面的更新。

声明式。数据变化后，React仅会更新变化的部分。

构建可复用的组件。通过 React 唯一要做的事情就是构建组件。得益于其良好的封装性，**组件使代码复用、测试和关注分离更加简单**。

## 二 基本概念

### 1 react方法及属性整理（以便用时快速查找）

[react方法及属性整理（以便用时快速查找）](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/reactfang-fa-ji-shu-xing-zheng-li-ff08-yi-bian-yong-shi-kuai-su-cha-zhao-ff09.md)

### 2 关于jsx

[关于jsx](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/guan-yu-jsx.md)

### 3 组件的props

[组件的props](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-de-props.md)

### 4 组件的state

[组件的state](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/zu-jian-de-state.md)

### 5 关于组件

[关于组件](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/guan-yu-zu-jian.md)

### 6 事件

[事件](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/shi-jian.md)

### 7 虚拟dom与访问dom

[虚拟dom与访问dom](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/xu-ni-dom.md)

### 8 数据流

[数据流](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/shu-ju-liu.md)

### 9 react性能优化

[react性能优化](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/reactxing-neng-you-hua.md)

### 10 Context

[Context](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/context.md)


### 11 react插件

[react插件](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/react/reactcha-jian.md)


## 三 使用及案例

代码位置：[https://github.com/chenhaoact/Front-End-Learn/tree/master/react-learn](https://github.com/chenhaoact/Front-End-Learn/tree/master/react-learn)

### 1 初始化一个react项目

要用 webpack 安装 React DOM 和构建你的包:

```
$ 
npm install --save react react-dom babel-preset-es2015 webpack
```

> 注意:这里如果你正在使用`babel-preset-es2015`支持 ES2015, 如果不需要支持ES2015，使用babel-preset-react包.

**注意:**默认情况下，React 将会在开发模式，很缓慢，不建议用于生产。要在生产模式下使用 React，设置环境变量`NODE_ENV`为`production`（使用 envify 或者 webpack's DefinePlugin）。例如：

```
new
 webpack.DefinePlugin({

"process.env"
: {
    NODE_ENV: JSON.stringify(
"production"
)
  }
});
```

2

## 四 资源与参考

### 1官网

react英文官网

[https://facebook.github.io/react/](https://facebook.github.io/react/)

react官方博客（包括重大版本的更新介绍）

[https://facebook.github.io/react/blog/all.html](https://facebook.github.io/react/blog/all.html)

react中文相关的网站：

React中国\(个人推荐的react中文学习网站，资料较新\)

[http://www.react-cn.com/](http://www.react-cn.com/)

React中文社区

[http://react-china.org/](http://react-china.org/)

### 2文档

英文文档（推荐）

[https://facebook.github.io/react/docs/hello-world.html](https://facebook.github.io/react/docs/hello-world.html)

中文文档（版本稍滞后于英文,适合快速入门，深入最好阅读英文档）

[http://www.react-cn.com/docs/getting-started.html](http://www.react-cn.com/docs/getting-started.html)

### 3源码

[https://github.com/facebook/react](https://github.com/facebook/react)

### 4教程

官方教程：

react英文教程（推荐）：

[https://facebook.github.io/react/tutorial/tutorial.html](https://facebook.github.io/react/tutorial/tutorial.html)

react中文教程

[http://www.react-cn.com/docs/tutorial.html](http://www.react-cn.com/docs/tutorial.html)

其他教程：

React 技术栈系列教程（阮一峰）

[http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html](http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html)

react官方推荐的articles and videos  
[https://github.com/facebook/react/wiki/Articles-and-Videos    ](https://github.com/facebook/react/wiki/Articles-and-Videos)  

React学习资源汇总

[https://github.com/facebook/react/wiki/Examples](https://github.com/facebook/react/wiki/Examples)

[https://github.com/tsrot/study-notes/blob/master/React学习资源汇总.md](https://github.com/tsrot/study-notes/blob/master/React学习资源汇总.md)

### 5工具与资源

react官方推荐的辅助工具插件库清单（包括各种组件库，脚手架，测试，调试等等，较全）  
[https://github.com/facebook/react/wiki/Complementary-Tools](https://github.com/facebook/react/wiki/Complementary-Tools)

react工具插件推荐（react中国）

[http://www.react-cn.com/addons/index.html](http://www.react-cn.com/addons/index.html)

react代码范例与demo（react中国）

[http://www.react-cn.com/docs/examples.html](http://www.react-cn.com/docs/examples.html)

