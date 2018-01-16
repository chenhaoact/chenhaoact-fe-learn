## 五 与其他异步处理方法的比较
### async 函数与 Promise、Generator 的比较：

假定某个 DOM 元素，部署一系列动画，前一个动画结束，才能开始后一个。有一个动画出错，就不再往下执行，返回上一个成功执行的动画的返回值。

（1）Promise 的写法：

```
function chainAnimationsPromise(elem, animations) {

  // 变量ret用来保存上一个动画的返回值
  let ret = null;

  // 新建一个空的Promise
  let p = Promise.resolve();

  // 使用then方法，添加所有动画
  for(let anim of animations) {
    p = p.then(function(val) {
      ret = val;
      return anim(elem);
    });
  }

  // 返回一个部署了错误捕捉机制的Promise
  return p.catch(function(e) {
    /* 忽略错误，继续执行 */
  }).then(function() {
    return ret;
  });

}
```


虽然 **Promise 的写法比回调函数的写法大大改进，但看上去，代码完全都是 Promise 的 API（then、catch等等），操作本身的语义反而不容易看出来**。

（2）Generator 函数的写法：

```
function chainAnimationsGenerator(elem, animations) {

  return spawn(function*() {
    let ret = null;
    try {
      for(let anim of animations) {
        ret = yield anim(elem);
      }
    } catch(e) {
      /* 忽略错误，继续执行 */
    }
    return ret;
  });

}
```


上面代码用 **Generator 函数**遍历每个动画，**语义比 Promise 写法更清晰**，用户定义的操作全出现在spawn函数内。这个写法的**问题在于，必须有一个任务运行器，自动执行 Generator 函数**，上面的spawn函数就是自动执行器，它返回 Promise 对象，且必须保证yield语句后的表达式，必须返回 Promise。

（3）async 函数的写法。



```
async function chainAnimationsAsync(elem, animations) {
  let ret = null;
  try {
    for(let anim of animations) {
      ret = await anim(elem);
    }
  } catch(e) {
    /* 忽略错误，继续执行 */
  }
  return ret;
}
```


**Async 函数的实现最简洁，最符合语义，几乎没有语义不相关的代码**。它**将 Generator 写法中的自动执行器，改在语言层面提供，不暴露给用户**，因此**代码量最少**。如用 Generator 写法，自动执行器需用户自己提供。

