## 中间件
Koa 的最大特色，也是最重要的一个设计，就是中间件。

在 Koa 和 Express 中，所有关于 HTTP 请求的事情都是在中间件内部完成的，最重要的则是理解中间件延续传递的概念.

中间件处在 HTTP Request 和 HTTP Response 中间，用来实现某种中间功能。app.use()用来加载中间件。


例子：


```
const logger = (ctx, next) => {
  console.log(`${Date.now()} ${ctx.request.method} ${ctx.request.url}`);
  next();
}
app.use(logger);
```



基本上，Koa 所有的功能都是通过中间件实现的。每个中间件默认接受两个参数，第一个参数是 Context 对象，第二个参数是next函数。只要调用next函数，就可以把执行权转交给下一个中间件。

### 洋葱圈模型：
####中间件栈
**多个中间件会形成一个栈结构，以"先进后出"的顺序执行。**

最外层的中间件首先执行。
调用next函数，把执行权交给下一个中间件。
...
最内层的中间件最后执行。
执行结束后，把执行权交回上一层的中间件。
...
最外层的中间件收回执行权之后，执行next函数后面的代码。

####洋葱圈模型具体参考：
https://eggjs.org/zh-cn/intro/egg-and-koa.html#middleware


## 参考
[Koa框架教程(阮一峰)](http://www.ruanyifeng.com/blog/2017/08/koa.html)


