# React重点整理

## 一 简介

### 1用途

### 2优缺点及对比

## 二 基本概念

## 三 使用及案例

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



## 四 资源

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

英文文档

[https://facebook.github.io/react/docs/hello-world.html](https://facebook.github.io/react/docs/hello-world.html)

中文文档（版本稍滞后于英文）

[http://www.react-cn.com/docs/getting-started.html](http://www.react-cn.com/docs/getting-started.html)

### 3源码

[https://github.com/facebook/react](https://github.com/facebook/react)

### 4教程

官方教程：

react英文教程（重要）：

[https://facebook.github.io/react/tutorial/tutorial.html](https://facebook.github.io/react/tutorial/tutorial.html)

react中文教程

[http://www.react-cn.com/docs/tutorial.html](http://www.react-cn.com/docs/tutorial.html)

其他教程：

React 技术栈系列教程（阮一峰）

[http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html](http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html)

React学习资源汇总

[https://github.com/tsrot/study-notes/blob/master/React学习资源汇总.md](https://github.com/tsrot/study-notes/blob/master/React学习资源汇总.md)

### 5工具与资源

react工具插件推荐（react中国）

[http://www.react-cn.com/addons/index.html](http://www.react-cn.com/addons/index.html)

react代码范例与demo（react中国）

[http://www.react-cn.com/docs/examples.html](http://www.react-cn.com/docs/examples.html)

