# Service Worker
## 一 简介
Service worker是一个**在浏览器后台运行的脚本，与网页不相干，专注于那些不需要网页或用户互动就能完成的功能。它主要用于操作离线缓存**。

### 特点：

属于JavaScript Worker，不能直接接触DOM，通过postMessage接口与页面通信。
不需要任何页面，就能执行。
不用的时候会终止执行，需要的时候又重新执行，即它是事件驱动的。
有一个精心定义的升级策略。
只在HTTPs协议下可用，这是因为它能拦截网络请求，所以必须保证请求是安全的。
可以拦截发出的网络请求，从而控制页面的网路通信。
内部大量使用Promise。

### 常见用途：
通过拦截网络请求，使得网站运行得更快，或者在**离线情况下，依然可以执行**。
作为**其他后台功能的基础，比如消息推送和背景同步**。

## 二 使用
TODO

## 参考
### 已学习


### 待学习
[《JavaScript 标准参考教程（alpha）》，阮一峰 Web API - Web Worker](http://javascript.ruanyifeng.com/htmlapi/webworker.html)

[MDN-Service Worker API](https://developer.mozilla.org/zh-CN/docs/Web/API/Service_Worker_API)


[从webWorker到serviceWorker](http://jixianqianduan.com/frontend-javascript/2014/06/05/webworker-serviceworker.html)