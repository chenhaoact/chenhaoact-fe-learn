# Weex学习总结

## 一 简介

### 1用途

一套简单易用的跨平台开发方案，能以 web 的开发体验构建高性能、可扩展的 native 应用，为了做到这些，Weex 与 Vue 合作，使用 Vue 作为上层框架，并遵循 W3C 标准实现了统一的 JSEngine 和 DOM API，这样一来，你甚至可以使用其他框架驱动 Weex，打造三端一致的 native 应用。

### 2优缺点及对比

## 二 基本概念

## 三 使用及案例

按照http://weex.apache.org/cn/guide/set-up-env.html安装weex最新的本地开发环境。



进入项目要存放的父级目录下，初始化一个 Weex 项目：

| weex init some-project |
| :--- |


执行完命令后，在`some-project`目录中就创建了一个使用 Weex 和 Vue 的模板项目。

  


进入项目所在路径，weex-toolkit 已经生成了标准项目结构：

在`package.json`中，已经配置好了几个常用的 npm script，分别是：

* `build`
  : 源码打包，生成 JS Bundle
* `dev`
  : webpack watch 模式，方便开发
* `serve`
  : 开启静态服务器
* `debug`
  : 调试模式

先通过`npm install`安装项目依赖。

之后要分别在两个命令窗中运行`npm run dev`和`npm run serve`开启watch 模式和静态服务器。

然后打开浏览器，进入`http://localhost:8080/index.html`即可看到 weex h5 页面。

初始化时已经创建了基本的示例，可以在`src/foo.vue`中查看。



Weex 语法可以直接参考[Vue Guide](https://vuejs.org/v2/guide/)



## 四 资源

### 1官网

weex新仓库迁移到了:

[https://github.com/apache/incubator-weex](https://github.com/apache/incubator-weex)

官网：

[https://weex.apache.org/](https://weex.apache.org/)



Weex 语法可以直接参考[Vue Guide](https://vuejs.org/v2/guide/)

### 2文档

### 3源码

### 4教程

官方教程：

[http://weex.apache.org/cn/guide/](http://weex.apache.org/cn/guide/)

其他教程：

### 5工具

Weex Native 运行时实例 & Weex 文件预览工具。

[https://weex.apache.org/cn/playground.html](https://weex.apache.org/cn/playground.html)

第三方开发组件工具类库市场（包括weex-chart等）

[https://market.dotwe.org/ext/list.htm](https://market.dotwe.org/ext/list.htm)

