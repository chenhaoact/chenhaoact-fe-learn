## 简介及基本写法

**async function 是语言层面提供的Generator 函数的语法糖**，由ES2017 标准引入，**它使得异步操作变得更加方便**。

**async译为异步的，await译为等待**。


### 1. 基本写法
**async函数就是将 Generator 函数的星号（*）替换成async，将yield替换成await，仅此而已**。


例子：
一个 Generator 函数，依次读取两个文件：



```
const fs = require('fs');

const readFile = function (fileName) {
  return new Promise(function (resolve, reject) {
    fs.readFile(fileName, function(error, data) {
      if (error) return reject(error);
      resolve(data);
    });
  });
};

const gen = function* () {
  const f1 = yield readFile('/etc/fstab');
  const f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```


gen写成async函数则如下：



```
const asyncReadFile = async function () {
  const f1 = await readFile('/etc/fstab');
  const f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```


### 2. 背景

**Node.js 是一个异步的世界，官方 API 支持的都是 callback 形式的异步编程模型，这会带来许多问题**，如

callback hell: 最臭名昭著的 callback 嵌套问题。
release zalgo: 异步函数中可能同步调用 callback 返回数据，带来不一致性。

因此社区提供了**各种异步的解决方案，最终胜出的是 Promise**，它也内置到了 ES2015 中。

而在 异步解决方案Promise 的基础上，结合 Generator 提供的切换上下文能力，出现了 co 等第三方类库来让我们**用同步写法编写异步代码**。同时，**async function 这个官方解决方案也于 ECMAScript 2017 中发布，并在 Node.js 8 中原生支持**。


### 3. async函数对 Generator 函数的改进，体现在四点 （重要）

####（1）内置执行器

**Generator 函数的执行必须靠执行器**，所以才有了co模块，**而async函数自带执行器。执行与普通函数一样，只需要后面加()**。



```
asyncReadFile();
```


上面代码调用了asyncReadFile函数，它就会自动执行，输出最后结果。这**完全不像 Generator 函数，需要调用next方法，或用co模块，才能真正执行，得到最后结果**。

####（2）更好的语义

async和await，**比起星号和yield，语义更清楚。async表示函数里有异步操作，await表示紧跟在后面的表达式需要等待结果**。

####（3）更广的适用性

co模块约定，yield命令后面只能是 Thunk 函数或 Promise 对象，**而async函数的await命令后面，可以是 Promise 对象和原始类型的值**（数值、字符串和布尔值，但这时等同于同步操作）。

####（4）返回值是Promise

**async函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了**。可用then方法指定下一步的操作。

进一步说，**async函数完全可看作多个异步操作，包装成的一个 Promise 对象，而await命令就是内部then命令的语法糖**。

