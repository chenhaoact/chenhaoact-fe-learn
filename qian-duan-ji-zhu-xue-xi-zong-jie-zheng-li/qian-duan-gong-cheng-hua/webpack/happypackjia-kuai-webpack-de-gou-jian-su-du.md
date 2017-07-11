# happypack-加快webpack的构建速度

## 一 简介

### 1用途
####（1）适用场景
加快webpack的构建速度（通过允许并行传输多个文件）

### 2优缺点及对比
####（1）优点

####（2）缺点


## 二 基本概念与技术重点整理


## 三 使用实践及案例

安装：



```
npm install --save-dev happypack

```


在webpack.config.js, 使用该插件：



```
var HappyPack = require('happypack');

exports.plugins = [
  new HappyPack({
    // loaders is the only required parameter:
    loaders: [ 'babel?presets[]=es2015' ],

    // customize as needed, see Configuration below
  })
];
```



用HappyPack的loader替换当前loaders:



```
exports.module = {
  loaders: {
    test: /.js$/,
    loaders: [ 'happypack/loader' ],
    include: [
      // ...
    ],
  }
};
```

这样这些文件就**会开启happypack来多进程并发的处理要构建打包的文件**。


HappyPack 加速第一招：多进程

Webpack 是个守旧的 js 工具，跟其他大部分 js 工具一样，是个单线程程序。js 执行效率本来就有一定的不足，又限定了单线程，速度自然快不到哪儿去。

然而 Webpack 这个工具强就强在流程设计的扩展性如此之强，可以人为的加上多进程处理。

HappyPack 加速第二招：缓存

HappyPack 实现了一个基本文件修改时间戳的缓存。在每次编译的同时会将每个源文件对应的编译结果缓存下来，同时记录下源文件的修改时间戳。**下次编译时，先读取源文件的修改时间戳，跟之前的缓存信息做对比，时间戳没有变化，则直接读取缓存文件作为 Loader 结果返回**。就是这么简单。

具体参考：
HappyPack - Webpack 的加速器
http://blog.yunfei.me/blog/happypack_webpack_booster.html



## 四 资源与参考

### 1官网

### 2文档

### 3源码

### 4教程
#### （1）已学习：



#### （2）学习中：



#### （3）待学习：
官方教程：
happypack
https://github.com/amireh/happypack

happypack各种场景下的例子
https://github.com/amireh/happypack/tree/master/examples

happypack webpack2
https://github.com/amireh/happypack/tree/master/examples/webpack2

其他教程：
HappyPack - Webpack 的加速器
http://blog.yunfei.me/blog/happypack_webpack_booster.html

happypack 原理解析
http://taobaofed.org/blog/2016/12/08/happypack-source-code-analysis/


### 5工具与资源

