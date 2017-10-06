# Page Visibility
## 一 简介
Page Visibility API，判断页面是否可见。它可以保证会在手机浏览器得到执行。
实际开发中，为了防止某些浏览器不支持这个 API，最好同时监听pagehide事件，这样会比较保险。

### 用途
通常，我们使用各种事件，判断用户是否正在离开当前页面。

visibilityState
pageshow
pagehide
beforeunload
unload

但是，**手机浏览器往往不会触发这些事件**，原因是浏览器进程会被突然关闭或者切换到后台，从而没有机会触发这些事件。常见的场景有以下这些。

用户点击了一条系统通知，切换到另一个 App。
用户进入任务切换窗口，切换到另一个 App。
用户点击了 Home 按钮，切换回主屏幕。
操作系统自动切换到另一个 App（比如，收到一个打入的电话）。

**上面这些情况，都会导致浏览器进程切换到后台，也很可能会被操作系统自动终止，以便回收资源。 这种情况下就要使用 Page Visibility API，判断页面是否可见**

## 二 使用
这个 API 部署在document对象上，提供以下两个属性。

document.hidden：返回一个布尔值，表示当前是否被隐藏。

**document.visibilityState**：表示页面当前的状态，可以取三个值。
visibile：页面可见
hidden：页面不可见
prerender：页面即将或正在渲染，不可见


## 参考
### 已学习

### 待学习
[拥抱HTML5 — Page Visibility(页面可见性) API介绍](http://www.cnblogs.com/zichi/p/5158745.html)

[《JavaScript 标准参考教程（alpha）》，阮一峰 Web API - Page Visibility API](http://javascript.ruanyifeng.com/htmlapi/pagevisibility.html)

[MDN - Page Visibility API](https://developer.mozilla.org/zh-CN/docs/Web/API/Page_Visibility_API)