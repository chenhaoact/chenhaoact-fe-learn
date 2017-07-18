# CommonJS规范

## 一 简介
**Node应用由模块组成，采用CommonJS模块规范。**

根据该规范，**每个文件就是一个模块，有自己的作用域。在一个文件里定义的变量、函数、类，都是私有的，对其他文件不可见**。

### 1用途
####（1）适用场景
Node.js主要用于服务器编程，模块文件一般都已经存在于本地硬盘，所以加载起来比较快，不用考虑非同步加载的方式，所以CommonJS规范比较适用。

### 2优缺点及对比
####（1）优点

####（2）缺点

####（3） 特点与对比
**module.exports导出模块，require（）加载导出的模块**

所有代码都运行在模块作用域，不会污染全局作用域。

**模块可以多次加载，但只会在第一次加载时运行一次，然后运行结果就被缓存**，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。

**模块加载的顺序，按照其在代码中出现的顺序。**

##### 和AMD的对比
**CommonJS规范加载模块是同步的，只有加载完成，才能执行后面的操作**。

**AMD规范则可以异步加载模块，允许指定回调函数**。

Node.js主要用于服务器编程，模块文件一般都已经存在于本地硬盘，所以加载起来比较快，不用考虑非同步加载的方式，所以CommonJS规范比较适用。

但**浏览器环境，要从服务器端加载模块，就必须采用非同步模式**，因此**浏览器端一般采用AMD规范**。

## 二 基本概念与技术重点整理

### （1）CommonJS模块基础
每个文件就是一个模块，有自己的作用域。在一个文件里定义的变量、函数、类，都是私有的，对其他文件不可见。

如果想在**多个文件分享变量，必须定义为global对象的属性**。如：


```
global.warning = true;

```

此写法不推荐。

**每个模块内部，module变量代表当前模块。**这个变量是一个对象，**它的exports属性（即module.exports）是对外接口。加载某个模块，其实是加载该模块的module.exports属性。**


例如：下面代码**通过module.exports导出模块**变量x和函数addX。


```
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;

```

通过下面代码**（require）加载导出的模块**：


```
var example = require('./example.js');

console.log(example.x); // 5
console.log(example.addX(1)); // 6

```


### （2）[CommonJS module对象](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qi-ta-ji-chu/commonjsgui-fan/moduledui-xiang.md)




## 三 使用实践及案例


## 四 资源与参考

### 1官网

### 2文档

### 3源码

### 4教程
#### （1）已学习：

CommonJS规范（阮一峰）
http://javascript.ruanyifeng.com/nodejs/module.html

#### （2）学习中：



#### （3）待学习：
官方教程：

其他教程：

### 5工具与资源







