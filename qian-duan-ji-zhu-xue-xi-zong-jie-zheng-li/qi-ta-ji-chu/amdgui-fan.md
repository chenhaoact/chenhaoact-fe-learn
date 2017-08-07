# AMD规范

## 一 简介

### 1. 为什么模块很重要？
**有了模块，就可以更方便地使用别人的代码，想要什么功能，就加载什么模块。**

但**前提是大家必须以同样的方式编写模块**。ES6之前通行的JS模块规范共有两种：CommonJS和[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)。


### 2. AMD诞生背景

在js模块规范出现之前，js可以使用（1）不同的函数（2）对象（3）立即执行函数（4）放大模式 等形式实现模块化，但各有缺点。具体可参考：[Javascript模块化编程（一）：模块的写法(阮一峰)](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)

**有了服务器端模块（nodejs的commonjs规范）以后，大家就想要客户端模块**。而且最好两者能兼容，一个模块不用修改，在服务器和浏览器都可以运行。

但**CommonJS规范不适用于浏览器环境，原因是：**

一个模块如果加载时间很长，整个应用就会停在那等。
对服务器端不是问题，因为所有模块都存放在本地硬盘，可同步加载完，等待时间是硬盘读取时间。但对浏览器却是大问题，模块都放在服务器端，等待时间取决于网速快慢，可能要等很长时间，浏览器处于"假死"状态。

因此，**浏览器端的模块，不能采用"同步加载"（synchronous），只能采用"异步加载"（asynchronous）**。这就是**AMD规范诞生**的背景。

### 3. AMD定义
AMD（Asynchronous Module Definition），意思是"异步模块定义"。它用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才运行。

AMD也用require()加载模块，但不同于CommonJS，它要求两参数：
　　

```
require([module], callback);

```

第一个参数[module]，是一个数组，里面的成员是要加载的模块；第二个参数callback，是加载成功之后的回调函数。

**[require.js](http://requirejs.org/)就是AMD规范的一种实现。**

### 1用途
####（1）适用场景
**AMD规范则可以异步加载模块，允许指定回调函数**。

**浏览器环境，要从服务器端加载模块，就必须采用非同步模式**，因此**浏览器端一般采用AMD规范**。



### 2优缺点及对比
####（1）优点

####（2）缺点

####（3）特点与对比


## 二 基本概念与技术重点整理

### （1）AMD模块规范基础
**AMD规范使用define方法定义模块**

### （2）[AMD规范的一种实现-require.js的用法](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qi-ta-ji-chu/amdgui-fan/requirejs.md)


## 三 使用实践及案例


## 四 资源与参考

### 1官网
[amdjs-api](https://github.com/amdjs/amdjs-api/wiki/AMD)

### 2文档

### 3源码

### 4教程
#### （1）已学习：

[Javascript模块化编程（一）：模块的写法(阮一峰)](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)

[Javascript模块化编程（二）：AMD规范 (阮一峰)](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)

#### （2）学习中：



#### （3）待学习：
官方教程：

其他教程：

### 5工具与资源



