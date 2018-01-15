## 二 语法

### 1. async函数返回一个 Promise 对象，可用then方法添加回调函数
当函数执行时，遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句

例子

async function getStockPriceByName(name) {
  const symbol = await getStockSymbol(name);
  const stockPrice = await getStockPrice(symbol);
  return stockPrice;
}

getStockPriceByName('goog').then(function (result) {
  console.log(result);
});
上面代码是一个获取股票报价的函数，函数前面的async关键字，表明该函数内部有异步操作。调用该函数时，会立即返回一个Promise对象。

另一个例子，指定多少毫秒后输出一个值：



```
function timeout(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint('hello world', 50);
```


上面代码指定 50 毫秒后，输出hello world。


### 2. await 命令
（1）在 **async function 中**，可**通过 await 关键字来等待一个 Promise 被 resolve（或 reject，此时会抛出异常）**， 

```
const fn = async function() {
  const user = await getUser();
  const posts = await fetchPosts(user.id);
  return { user, posts };
};
fn().then(res => console.log(res)).catch(err => console.error(err.stack));
```

（2）正常情况，await命令后是一个 Promise 对象。如不是会被转成一个立即resolve的 Promise 对象。



```
async function f() {
  return await 123;
}

f().then(v => console.log(v))
// 123
```


上面代码，await命令的参数是数值123，它被转成 Promise 对象，并立即resolve。

（3）**await命令后面的 Promise 对象如果变为reject状态，则reject的参数会被catch方法的回调函数接收到**。



```
async function f() {
  await Promise.reject('出错了');
}

f()
.then(v => console.log(v))
.catch(e => console.log(e))
// 出错了
```


上面代码，await语句前没有return，但reject方法的参数依然传入了catch方法的回调函数。这里如在await前加return，效果一样。

（4）**只要一个await语句后的 Promise 变为reject，整个async函数都会中断执行**

async function f() {
  await Promise.reject('出错了');
  await Promise.resolve('hello world'); // 不会执行
}

上面代码中，第二个await语句不会执行，因为第一个await语句状态变成了reject。

有时，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个await放在try...catch结构里面，这样不管这个异步操作是否成功，第二个await都会执行。

async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
  }
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// hello world
另一种方法是await后面的 Promise 对象再跟一个catch方法，处理前面可能出现的错误。

async function f() {
  await Promise.reject('出错了')
    .catch(e => console.log(e));
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// 出错了
// hello world


### 3. async 函数有多种使用形式



```
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)

// Class 的方法
class Storage {
  constructor() {
    this.cachePromise = caches.open('avatars');
  }

  async getAvatar(name) {
    const cache = await this.cachePromise;
    return cache.match(`/avatars/${name}.jpg`);
  }
}

const storage = new Storage();
storage.getAvatar('jake').then(…);

// 箭头函数
const foo = async () => {};
```

### 4. async函数的语法规则的难点 —— 错误处理机制

（1）**async函数**返回一个 Promise 对象，它**内部return语句返回的值，会成为then方法回调函数的参数**。


```

async function f() {
  return 'hello world';
}

f().then(v => console.log(v))
// "hello world"
```


上面代码，函数f内return返回的值，会被then方法回调函数接收到。

（2）**async函数内抛出错误，会导致返回的 Promise 对象变为reject状态。抛出的错误对象会被catch方法回调函数接收到**。



```
async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log(v),
  e => console.log(e)
)
// Error: 出错了
```


（3）如果**await后面的异步操作出错，等同于async函数返回的 Promise 对象被reject**

例如：

```
async function f() {
  await new Promise(function (resolve, reject) {
    throw new Error('出错了');
  });
}

f()
.then(v => console.log(v))
.catch(e => console.log(e))
// Error：出错了
```

**防止出错的方法，也是将其放在try...catch代码块中**。



```
async function f() {
  try {
    await new Promise(function (resolve, reject) {
      throw new Error('出错了');
    });
  } catch(e) {
  }
  return await('hello world');
}
```


（4）**如有多个await，可统一放在try...catch中进行错误处理**



```
async function main() {
  try {
    const val1 = await firstStep();
    const val2 = await secondStep(val1);
    const val3 = await thirdStep(val1, val2);

    console.log('Final: ', val3);
  }
  catch (err) {
    console.error(err);
  }
}
```


### 5. Promise 对象的状态变化
**async函数返回的 Promise 对象，必须等到内部所有await命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到return语句或者抛错**。即：只有**async函数内部的异步操作执行完，才会执行then方法指定的回调函数**。

例子



```
async function getTitle(url) {
  let response = await fetch(url);
  let html = await response.text();
  return html.match(/<title>([\s\S]+)<\/title>/i)[1];
}
getTitle('https://tc39.github.io/ecma262/').then(console.log)
// "ECMAScript 2017 Language Specification"
```


上面代码，函数getTitle内有三操作：抓取网页、取出文本、匹配页面标题。只有这三操作全完成，才执行then方法里的console.log。

