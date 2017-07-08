# TODO

## 一 简介
**Babel** 是一个 **JS 编译器**。可以让今天就用下一代 JavaScript 语法写代码并**仍然可以在旧的浏览器中运行**。（可以支持各种环境，如webpack,browserify，gulp等）




### 1用途
####（1）适用场景


### 2优缺点及对比
####（1）优点

####（2）缺点


## 二 基本概念与技术重点整理

## 三 使用实践及案例
latest已经被弃用，想使用最新版的es6的支持要使用env（比如像支持2017年想支持es2017）:

https://babeljs.io/docs/plugins/preset-env/

```
npm install babel-preset-env --save-dev
```



创建.babelrc

配置如下声明babel行为

```
{
"presets":["env"]
}
```

.babelrc文件使用和配置方法
https://babeljs.io/docs/usage/babelrc/


 

## 四 资源与参考

### 1官网
[https://babeljs.io/](https://babeljs.io/)
[http://babeljs.cn/](http://babeljs.cn/)



### 2文档

### 3源码

### 4教程
#### （1）已学习：



#### （2）学习中：



#### （3）待学习：
官方教程：

其他教程：
.babelrc文件使用和配置方法
https://babeljs.io/docs/usage/babelrc/

在各种环境下使用babel:

[http://babeljs.cn/docs/setup/](http://babeljs.cn/docs/setup/)

可以好好研究下babel源代码，看下是如何实现es6转es5的，对理解es6和es5很有好处：

[https://github.com/babel/babel](https://github.com/babel/babel)

babel官网的es2015教程（推荐）

[https://babeljs.io/learn-es2015/](https://babeljs.io/learn-es2015/)

babel相关插件

[https://babeljs.io/docs/plugins/](https://babeljs.io/docs/plugins/)

Babel 入门教程
http://www.ruanyifeng.com/blog/2016/01/babel.html

### 5工具与资源

