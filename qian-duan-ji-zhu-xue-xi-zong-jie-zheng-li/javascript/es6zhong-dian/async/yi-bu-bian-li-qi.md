## 七 异步遍历器 

遍历器 Iterator 接口是一种数据遍历的协议，只要调用遍历器对象的next方法，就会得到一个对象，表示当前遍历指针所在位置的信息。next方法返回的对象的结构是{value, done}，其中value表示当前数据的值，done布尔值表示遍历是否结束。

这里**隐含着规定，Iterator遍历器对象的next方法必须是同步的，只要调用就必须立刻返回值。一旦执行next方法，就必须同步地得到value和done**。如遍历指针正好指向同步操作，没有问题，但**对异步操作，就不合适了**。

**目前的解决方法是，Generator 函数里面的异步操作，返回一个 Thunk 函数或 Promise 对象**，即value属性是一个 Thunk 函数或 Promise 对象，等待以后返回真正的值，而done属性则还是同步产生的。

目前，有一个[提案](https://github.com/tc39/proposal-async-iteration)，**为异步操作提供原生的遍历器接口，即value和done这两属性都是异步产生，称为”异步遍历器“（Async Iterator）**。


### 该提案异步遍历器（asyncIterator）的接口
**异步遍历器的最大的语法特点，是调用遍历器的next方法，返回的是 Promise 对象：**



```
asyncIterator
  .next()
  .then(
    ({ value, done }) => /* ... */
  );
```

异步遍历器详细特性如：
for await...of 循环
yield* 语句 （可以跟一个异步遍历器）

请参考：
http://es6.ruanyifeng.com/#docs/async#异步遍历器
