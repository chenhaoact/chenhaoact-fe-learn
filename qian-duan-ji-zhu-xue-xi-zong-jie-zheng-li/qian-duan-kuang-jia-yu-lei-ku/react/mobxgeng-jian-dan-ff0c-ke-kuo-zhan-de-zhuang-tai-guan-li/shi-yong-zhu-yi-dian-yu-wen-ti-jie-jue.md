### 一 组件重复使用而不能记录上次数据则需要在组件不渲染时重置状态，否则会出现下一次重新进入时页面数据的污染
页面状态数据会存储，如果组件会返回再进入而不能记录原来数据（比如文章，商品的详情页），需要把数据在组件销毁前重置，最好写一个 reset（），在组件 componentWillUnmount时调用：


在model文件里：
```

@action reset() {
  transaction(() => {
    this.data1 = data1初始值；
    this.data1 = data2初始值；
  })
}
```

在组件里：



```
componentWillUnmount(){
  model.reset();
}
```





