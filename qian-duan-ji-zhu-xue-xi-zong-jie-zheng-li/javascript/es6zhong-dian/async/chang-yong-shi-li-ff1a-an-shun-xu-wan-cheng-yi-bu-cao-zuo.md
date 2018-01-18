## 六 常用实例：按顺序完成异步操作

实际开发经常遇到**一组异步操作，需按照顺序完成**。如，依次远程读取一组 URL，再按照读取顺序输出结果。

Promise 的写法（略）不太直观，可读性差。下面是 **async 函数实现**：



```
async function logInOrder(urls) {
  for (const url of urls) {
    const response = await fetch(url);
    console.log(await response.text());
  }
}
```


**上面代码确实大大简化，问题是所有远程操作都是继发。只有前一个返回结果，才会去读取下一个，这样效率差，非常浪费时间**。我们**需要的是并发发出远程请求**：



```
async function logInOrder(urls) {
  // 并发读取远程URL
  const textPromises = urls.map(async url => {
    const response = await fetch(url);
    return response.text();
  });

  // 按次序输出
  for (const textPromise of textPromises) {
    console.log(await textPromise);
  }
}
```


上面代码中，虽然**map方法的参数是async函数，但它是并发执行的，因为只有async函数内是继发执行，外部不受影响。后面的for..of循环内使用await，实现了按顺序输出**。