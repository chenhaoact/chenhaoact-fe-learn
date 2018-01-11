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


### 2. 在 **async function 中**，可**通过 await 关键字来等待一个 Promise 被 resolve（或者 reject，此时会抛出异常）**， 

```
const fn = async function() {
  const user = await getUser();
  const posts = await fetchPosts(user.id);
  return { user, posts };
};
fn().then(res => console.log(res)).catch(err => console.error(err.stack));
```

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

### async函数的语法规则的难点是错误处理机制

**async函数**返回一个 Promise 对象，它**内部return语句返回的值，会成为then方法回调函数的参数**。

async function f() {
  return 'hello world';
}

f().then(v => console.log(v))
// "hello world"
上面代码中，函数f内部return命令返回的值，会被then方法回调函数接收到。

async函数内部抛出错误，会导致返回的 Promise 对象变为reject状态。抛出的错误对象会被catch方法回调函数接收到。

async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log(v),
  e => console.log(e)
)
// Error: 出错了


