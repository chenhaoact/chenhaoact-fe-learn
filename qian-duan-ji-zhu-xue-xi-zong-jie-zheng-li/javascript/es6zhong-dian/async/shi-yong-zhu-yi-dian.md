## 三 使用注意点
### 1. await命令后的Promise对象，运行结果可能是rejected，所以最好把await命令放在try...catch代码块中



```
async function myFunction() {
  try {
    await somethingThatReturnsAPromise();
  } catch (err) {
    console.log(err);
  }
}
```




### 2. 多个await命令后的异步操作，如果不存在继发关系（继发指触发需要有先后顺序），最好让它们同时触发



```
let foo = await getFoo();
let bar = await getBar();
```

上面代码中，getFoo和getBar是**两个独立的异步操作（即互不依赖），被写成继发关系，比较耗时，因为只有前面的完成以后，才会执行后面的，完全可以让它们同时触发**：



```
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```



上面两种写法，getFoo和getBar都同时触发，**这样能缩短程序的执行时间**。



### 3. await命令只能用在async函数中，如用在普通函数，会报错

如果确实希望多个请求并发执行，可以使用Promise.all方法。
