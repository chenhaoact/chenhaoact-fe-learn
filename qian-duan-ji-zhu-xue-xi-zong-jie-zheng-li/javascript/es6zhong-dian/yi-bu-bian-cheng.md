# js异步编程

## 一 js的单线程与同步异步

### 单线程
js语言的执行环境是"单线程"的。
即一次只能完成一件任务。如有多个任务，须排队，

好处：
实现起来比较简单，执行环境相对不那么复杂；

坏处：
只要有一个任务耗时很长，后面的任务都必须排队等着，会拖延整个程序的执行。常见的浏览器无响应（假死），往往是因为某一段Js代码长时间运行（如死循环），导致整个页面卡住。

### 同步、异步模式
为了上述问题，Js语言将任务的执行模式分成两种：同步（**Sync**hronous）和**异步**（**Async**hronous）。

同步模式：
就是上面的模式，后一个任务等待前一个任务结束，然后再执行；

异步模式：
**每个任务有一或多个回调函数（callback），前一个任务结束后，不是执行后一个任务，而是执行回调函数，后一个任务则是不等前一个任务结束就执行**，所以**程序的执行顺序与任务的排列顺序是不一致的、异步的**。

"异步模式"非常重要。**在浏览器端，耗时很长的操作都应该异步执行，避免浏览器失去响应，最好的例子就是Ajax操作**。

在**服务器端，"异步模式"甚至是唯一的模式**，因为执行环境是单线程的，如果允许同步执行所有http请求，服务器性能会急剧下降，很快就会失去响应。

上面是js语言的特性与规范，下面是用js"异步模式"进行编程的几种常用方法：

## 二 js异步编程的几种方法
### 1. 回调函数

这是异步编程最基本的方法。（**回调函数就是把函数（如f2）作为参数传入函数(如f1)中，在该函数（f1）中可以执行作为参数传入的函数(f2)，f2称为回调函数**）

假定有两函数f1和f2，后者等待前者的执行结果。
　

```
　f1();
　f2();
```

如果f1很耗时，可以把f2改写成f1的回调函数。


```
　function f1(callback){
　　　　setTimeout(function () {
　　　　　　// f1的任务代码
　　　　　　callback();
　　　　}, 1000);
　　}
```


执行代码时变成这样：
`　f1(f2);`

**采用回调函数这种方式，把同步操作变成了异步操作，f1不会堵塞程序运行，相当于先执行程序的主要逻辑，将耗时的操作（f1及依赖其结果才能执行的f2）推迟执行**。

优点：简单、容易理解和部署

缺点：不利于代码的阅读和维护，各部分间高耦合，流程会很混乱，**且每个任务只能指定一个回调函数**。

### 2. 事件监听
任务的执行不取决于代码的顺序，而取决于某个事件是否发生。

具体使用略。

### 3. 发布/订阅
假定存在一个"信号中心"，某任务执行完成，就向信号中心"发布"一个信号，其他任务可以向信号中心"订阅"（subscribe）这个信号，从而知道什么时候自己可以开始执行。这就叫做**"发布/订阅模式"（publish-subscribe pattern），又称"观察者模式"（observer pattern）**。

具体使用略。

### 4. Promises对象
具体见下面

## 三 promise对象（重点）
### 1. 简介
**Promise 是异步编程的一种解决方案**，比传统的解决方案（回调函数和事件）更合理和更强大。**最早由（ CommonJS）提出**和实现，**ES6 将其写进了语言标准，统一了用法，原生提供了Promise对象**。

首先，Promise是一个对象，与其他Js对象的用法没什么两样；其次，**它起到代理作用（proxy），充当异步操作与回调函数之间的中介。它使得异步操作具备同步操作的接口，让程序具备正常的同步运行的流程，回调函数不必再一层层嵌套。**

每一个异步任务立刻返回一个Promise对象，由于是立刻返回，所以可以采用同步操作的流程。这个Promises对象有一个then方法，允许指定回调函数，在异步任务完成后调用。

比如，异步操作f1返回一个Promise对象，它的回调函数f2写法如下：

```
(new Promise(f1)).then(f2);

```
**这种写法对于多层嵌套的回调函数尤其方便**。

### 2.Promise接口
**Promise的基本思想**是，异步任务返回一个Promise对象。

**Promise对象只有三种状态**：

异步操作**“未完成”（pending）**
异步操作**“已完成”（resolved**，又称fulfilled）
异步操作**“失败”（rejected）**

**三种状态的变化途径只有两种**：

异步操作从**“未完成”到“已完成”**
异步操作从**“未完成”到“失败”**。

这种变化只能发生一次，一旦当前状态变为“已完成”或“失败”，就不会再有新的状态变化。因此，**Promise对象的最终结果只有两种**。

**异步操作成功**，Promise对象传回一个值，状态变为resolved。

**异步操作失败**，Promise对象抛出一个错误，状态变为rejected。

#### then方法
**Promise对象使用then方法添加回调函数：**
**then方法可接受两个回调函数，第一个是异步操作成功时（变为resolved状态）时的回调函数，第二个是异步操作失败（变为rejected）时的回调函数（可省略）。一旦状态改变，就调用相应的回调函数。**

then方法可链式使用。

```
// po是一个Promise对象
po.then(step1)
  .then(step2)
  .then(step3)
  .then(
    console.log,
    console.error
  );
```
po的状态一旦变为resolved，就依次调用后面每个then指定的回调函数，**每一步都必须等到前一步完成，才会执行**。最后一个then方法的回调函数console.log和console.error，用法上有重要区别：console.log只显示回调函数step3的返回值，而**最后一个then的未完成回调函数(这里是console.error)可以显示step1、step2、step3之中任意一个发生的错误**。也就是说，**若step1操作失败，抛出一个错误，这时step2和step3都不会再执行了（因为它们是操作成功的回调函数（作为第一个参数）**，而不是操作失败的回调函数）。**Promises对象开始寻找，接下来第一个操作失败时的回调函数并执行它**，在上面代码中是console.error。这就是说，**Promises对象的错误有传递性。**

从同步的角度看，上面的代码大致等同于下面的形式。


```
try {
  var v1 = step1(po);
  var v2 = step2(v1);
  var v3 = step3(v2);
  console.log(v3);
} catch (error) {
  console.error(error);
}
```

#### Promise对象的生成（Promise构造函数： Promise（））
Promise构造函数，**用来生成Promise实例**。

**下面代码创造一个Promise实例：
**

```
var promise = new Promise(function(resolve, reject) {
  // 异步操作的代码

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由Js提供，不用自己部署。

**resolve函数的作用:**
将Promise对象的状态从“未完成”变为“成功”（即从Pending变为Resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；

**reject函数的作用:**
将Promise对象的状态从“未完成”变为“失败”（即从Pending变为Rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

**Promise实例生成以后，可以用then方法分别指定Resolved状态和Reject状态的回调函数**。

```
po.then(function(value) {
  // success
}, function(value) {
  // failure
});
```

### 3. Promise应用（重点）
#### Ajax操作
Ajax操作是典型的异步操作,使用Promise对象，可以写成:

```
function search(term) {
  var url = 'http://example.com/search?q=' + term;
  var xhr = new XMLHttpRequest();
  var result;

  var p = new Promise(function (resolve, reject) {
    xhr.open('GET', url, true);
    xhr.onload = function (e) {
      if (this.status === 200) {
        result = JSON.parse(this.responseText);
        resolve(result);
      }
    };
    xhr.onerror = function (e) {
      reject(e);
    };
    xhr.send();
  });

  return p;
}

search("Hello World").then(console.log, console.error);

```

**这里最后一行调用时，search返回一个promise对象，对他执行then方法，指定了成功的resolve方法（为console.log），失败的reject（console.error），这两个具体的方法会替换掉new Promise(）定义中的resolve和reject在Promise(）里面的异步逻辑中具体执行。**

### 4. Promise的优缺点

#### 优点：
**让回调函数变成了规范的链式写法，程序流程可以看得很清楚。**它的一整套接口，可以实现许多强大的功能，比如为多个异步操作部署一个回调函数、为多个回调函数中抛出的错误统一指定处理方法等。

而且，**它还有一个前面三种方法都没有的好处：如果一个任务已经完成，再添加回调函数，该回调函数会立即执行。不用担心是否错过了某个事件或信号**。

#### 缺点：
**编写和理解都相对比较难。**


## 参考：
### 已学习
[Javascript异步编程的4种方法（阮一峰）](http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html)

[《Javascript标准参考教程》-Promise对象](http://javascript.ruanyifeng.com/advanced/promise.html#toc6)

### 待学习
[Node.js回调黑洞全解：Async、Promise 和 Generator](https://zhuanlan.zhihu.com/p/19750470)

[《ECMAScript 6 入门》-Promise对象](http://es6.ruanyifeng.com/#docs/promise)