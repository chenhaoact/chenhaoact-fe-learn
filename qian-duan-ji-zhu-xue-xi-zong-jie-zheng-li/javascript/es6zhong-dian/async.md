# async 函数

背景：

**Node.js 是一个异步的世界，官方 API 支持的都是 callback 形式的异步编程模型，这会带来许多问题**，如

callback hell: 最臭名昭著的 callback 嵌套问题。
release zalgo: 异步函数中可能同步调用 callback 返回数据，带来不一致性。

因此社区提供了**各种异步的解决方案，最终胜出的是 Promise**，它也内置到了 ECMAScript 2015 中。

而在 Promise 的基础上，结合 Generator 提供的切换上下文能力，出现了 co 等第三方类库来让我们**用同步写法编写异步代码**。同时，**async function 这个官方解决方案也于 ECMAScript 2017 中发布，并在 Node.js 8 中原生支持**。

 
## 简介

async function 是语言层面提供的语法糖，在 **async function 中**，我们可以**通过 await 关键字来等待一个 Promise 被 resolve（或者 reject，此时会抛出异常）**， 

```
const fn = async function() {
  const user = await getUser();
  const posts = await fetchPosts(user.id);
  return { user, posts };
};
fn().then(res => console.log(res)).catch(err => console.error(err.stack));
```



