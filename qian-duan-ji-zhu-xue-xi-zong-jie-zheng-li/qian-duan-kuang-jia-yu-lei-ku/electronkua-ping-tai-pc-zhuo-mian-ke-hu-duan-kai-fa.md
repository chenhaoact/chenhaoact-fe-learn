# electron-跨平台PC桌面客户端开发

## 一 简介

### 1用途

Build cross platform desktop apps with JavaScript, HTML, and CSS

### 2优缺点及对比

Electron 可以让你使用纯 JavaScript 调用丰富的原生 APIs 来创造桌面应用，可以把它看作一个专注于桌面应用的 Node.js 的变体。

不意味着 Electron 是绑定了 GUI 库的 JavaScript。相反，Electron 使用 web 页面作为它的 GUI，所以你能把它看作成一个被 JavaScript 控制的，精简版的 Chromium 浏览器。

## 二 基本概念

### 主进程

在 Electron 里，运行`package.json`里`main`脚本的进程被称为**主进程**。在主进程运行的脚本可以以创建 web 页面的形式展示 GUI。

### 渲染进程

由于 Electron 使用 Chromium 展示页面，Chromium 的多进程结构也被充分利用。每个 Electron 的页面都运行着自己的进程，这样的进程为**渲染进程**。

一般浏览器中，网页通常在沙盒环境下运行，不允许访问原生资源。而Electron 用户拥有在网页中调用 Node.js 的 APIs 的能力，可以与底层操作系统直接交互。

### 主进程与渲染进程的区别

**主进程使用**`BrowserWindow`**实例创建页面。每个**`BrowserWindow`**实例都在自己的渲染进程里运行页面**。当一个`BrowserWindow`实例被销毁后，相应的渲染进程也会被终止。

主进程管理所有页面和与之对应的渲染进程。每个渲染进程都是相互独立的，并只关心他们自己的页面。

由于**在页面里管理原生 GUI 资源非常危险而且易造成资源泄露，所以在页面调用 GUI 相关的 APIs 是不被允许的。如果想在网页里使用 GUI 操作，其对应的渲染进程必须与主进程进行通讯，请求主进程进行相关的 GUI 操作。**

在 Electron，我们**提供几种方法用于主进程和渲染进程之间的通讯**。像[`ipcRenderer`](https://github.com/electron/electron/blob/master/docs-translations/zh-CN/api/ipc-renderer.md)和[`ipcMain`](https://github.com/electron/electron/blob/master/docs-translations/zh-CN/api/ipc-main.md)模块用于发送消息，[remote](https://github.com/electron/electron/blob/master/docs-translations/zh-CN/api/remote.md)模块用于 RPC 方式通讯。这些内容都可以在一个 FAQ 中查看[how to share data between web pages](https://github.com/electron/electron/blob/master/docs-translations/zh-CN/faq.md#how-to-share-data-between-web-pages)。

## 三 使用实践及案例

首先，按照官方中文文档的[快速入门](https://github.com/electron/electron/blob/master/docs-translations/zh-CN/tutorial/quick-start.md)搭建一个electron应用：

大体上，一个 Electron 应用的目录结构如下：

```
your-app/
├── package.json
├── main.js
└── index.html

```

`package.json`的格式和 Node 的完全一致，并且那个被`main`字段声明的脚本文件\(建议写为main.js\)是你的应用的启动脚本，它运行在主进程上。

**注意**：如果`main`字段没有在`package.json`声明，Electron会优先加载`index.js`。

`main.js`应该用于创建窗口和处理系统事件，初始案例例填写如下：



```
const {app, BrowserWindow} = require('electron')
const path = require('path')
const url = require('url')

// 保持一个对于 window 对象的全局引用，如果你不这样做，
// 当 JavaScript 对象被垃圾回收， window 会被自动地关闭
let win

function createWindow () {
  // 创建浏览器窗口。
  win = new BrowserWindow({width: 800, height: 600})

  // 加载应用的 index.html。
  win.loadURL(url.format({
    pathname: path.join(__dirname, 'index.html'),
    protocol: 'file:',
    slashes: true
  }))

  // 打开开发者工具。
  win.webContents.openDevTools()

  // 当 window 被关闭，这个事件会被触发。
  win.on('closed', () => {
    // 取消引用 window 对象，如果你的应用支持多窗口的话，
    // 通常会把多个 window 对象存放在一个数组里面，
    // 与此同时，你应该删除相应的元素。
    win = null
  })
}

// Electron 会在初始化后并准备
// 创建浏览器窗口时，调用这个函数。
// 部分 API 在 ready 事件触发后才能使用。
app.on('ready', createWindow)

// 当全部窗口关闭时退出。
app.on('window-all-closed', () => {
  // 在 macOS 上，除非用户用 Cmd + Q 确定地退出，
  // 否则绝大部分应用及其菜单栏会保持激活。
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // 在这文件，你可以续写应用剩下主进程代码。
  // 也可以拆分成几个文件，然后用 require 导入。
  if (win === null) {
    createWindow()
  }
})

// 在这文件，你可以续写应用剩下主进程代码。
// 也可以拆分成几个文件，然后用 require 导入。

```

创建展示页面index.html如下：


```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using node <script>document.write(process.versions.node)</script>,
    Chrome <script>document.write(process.versions.chrome)</script>,
    and Electron <script>document.write(process.versions.electron)</script>.
  </body>
</html>
```

然后，全局安装electron：


```
npm install -g electron

```

安装如果出现问题，多事由于网络原因，可以使用淘宝的cnpm安装（淘宝npm详细参考：https://npm.taobao.org/）：


```
cnpm install -g electron

```


在刚刚所创建的项目下安装electron：



```
cnpm install --save-dev electron
```

在package.json中的scripts中添加如下内容：



```
"scripts": {
    "start": "electron ."
  },
```

然后执行命令：



```
npm start
```

就可以运行刚刚创建的electron应用了，会出现一个桌面应用，页面右边还有chrome的调试工具，效果如下：


![](/assets/QQ20170605-212226@2x.png)


  


## 四 资源

### 1官网

[https://electron.atom.io/](https://electron.atom.io/)

electron官网博客

[https://electron.atom.io/blog/](https://electron.atom.io/blog/)

electron官网社区（包含一些工具，组件，学习视频资源等）

[https://electron.atom.io/community/](https://electron.atom.io/community/)

**electron开发生态系统中用到最多的包和依赖以及最活跃的的开发者和开源项目排名（能找到很多资源）：**

[https://electron.atom.io/userland/](https://electron.atom.io/userland/)

用electron搭建的一些应用（可以找到源代码）

[https://electron.atom.io/apps/](https://electron.atom.io/apps/)

最受开发者关注的一些electron应用（可以找到源代码）

[https://electron.atom.io/userland/starred\_apps](https://electron.atom.io/userland/starred_apps)

### 2文档

英文文档

[https://electron.atom.io/docs/](https://electron.atom.io/docs/)

中文文档

[https://github.com/electron/electron/tree/master/docs-translations/zh-CN](https://github.com/electron/electron/tree/master/docs-translations/zh-CN)

### 3源码

[https://github.com/electron/electron](https://github.com/electron/electron)

### 4教程

官方教程：

electron快速入门

[https://github.com/electron/electron/blob/master/docs-translations/zh-CN/tutorial/quick-start.md](https://github.com/electron/electron/blob/master/docs-translations/zh-CN/tutorial/quick-start.md)

完整英文教程
[https://electron.atom.io/docs/guides/](https://electron.atom.io/docs/guides/)

其他教程：

electron中文教程（gitbook）

[https://weishuai.gitbooks.io/electron-/content/](https://weishuai.gitbooks.io/electron-/content/)

