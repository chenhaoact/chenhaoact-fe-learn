# Web Worker 与
## 一 简介
Web Worker 是HTML5标准的一部分，这一规范定义了一套 API，**它允许一段Js程序运行在主线程之外的另外一个线程中**。

Web Worker 规范中定义了**两类工作线程，分别是专用线程Dedicated Worker(只能为一个页面所使用)和共享线程 Shared Worker(可以被多个页面所共享)**。

### Web Worker的几个特点：

**同域限制。**子线程加载的脚本文件，必须与主线程的脚本文件在同一个域。

DOM限制。**子线程所在的全局对象，与主进程不一样，它无法读取网页的DOM对象**，即document、window、parent这些对象，子线程都无法得到。（但是，navigator对象和location对象可以获得。）

脚本限制。**子线程无法读取网页的全局变量和函数，也不能执行一些方法**如：alert和confirm等，不过可以执行setTimeout等，以及使用XMLHttpRequest对象发出AJAX请求。

文件限制。子线程无法读取本地文件，即**子线程无法打开本机的文件系统**（file://），它**所加载的脚本，必须来自网络**。

## 二 使用
### 1. 新建和启动子线程
主线程采用new命令，调用Worker构造函数，可以新建一个子线程。


```
var worker = new Worker('work.js');

```

### 2. 主线程与子线程的数据通信
子线程新建之后，并没有启动，必需等待主线程调用**postMessage方法**，即发出信号之后才会启动。postMessage方法的参数，就是主线程传给子线程的信号。它可以是一个字符串，也可以是一个对象。



```
worker.postMessage("Hello World");
worker.postMessage({method: 'echo', args: ['Work']});
```

### 3. 子线程与主线程的事件监听
子线程和主线程都可以使用addEventListener来注册事件。

#### 子线程的事件监听
在子线程内，必须有一个回调函数，监听message事件。



```
/* File: work.js */

self.addEventListener('message', function(e) {
  self.postMessage('You said: ' + e.data);
}, false);
```



**self代表子线程自身，self.addEventListener表示对子线程的message事件指定回调函数**（直接指定onmessage属性的值也可）。回调函数的参数是一个事件对象，它的data属性包含主线程发来的信号。**self.postMessage则表示，子线程向主线程发送一个信号。**

根据主线程发来的不同的信号值，子线程可以调用不同的方法。



```
/* File: work.js */

self.onmessage = function(event) {
  var method = event.data.method;
  var args = event.data.args;

  var reply = doSomething(args);
  self.postMessage({method: method, reply: reply});
};

```


#### 主线程的事件监听
主线程也必须指定message事件的回调函数，监听子线程发来的信号。



```
/* File: main.js */

worker.addEventListener('message', function(e) {
	console.log(e.data);
}, false);
```




### 4. 关闭子线程

使用完毕之后，为了节省系统资源，我们必须在主线程调用terminate方法，手动关闭子线程。



```
worker.terminate();

```

也可以子线程内部关闭自身。



```
self.close();

```


## 参考
### 已学习


### 待学习
[《JavaScript 标准参考教程（alpha）》，阮一峰 Web API - Web Worker](http://javascript.ruanyifeng.com/htmlapi/webworker.html)

[MDN-Web Workers API](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API)

[深入理解Web Worker - AlloyTeam](http://www.alloyteam.com/2015/11/deep-in-web-worker/)

[从webWorker到serviceWorker](http://jixianqianduan.com/frontend-javascript/2014/06/05/webworker-serviceworker.html)