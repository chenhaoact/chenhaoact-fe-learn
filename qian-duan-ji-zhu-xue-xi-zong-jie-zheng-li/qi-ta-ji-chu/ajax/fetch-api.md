# Fetch API
## 一 简介
Ajax操作所用的XMLHttpRequest对象，已有十多年历史，其API设计并不是很好，输入、输出、状态都在同一个接口管理，容易写出混乱的代码。

**Fetch API是一种新规范，用来取代XMLHttpRequest对象。**

### Fetch API相比于Ajax的优点
它主要有**两个特点，一是接口合理化**，Ajax是将所有**不同性质的接口**都放在XHR对象上，而Fetch是将它们**分散在几个不同的对象上**，设计更合理；**二是Fetch操作返回Promise对象，避免了嵌套的回调函数**。

Fetch API最大的特点：除了返回Promise对象，还有一点就是**数据传送是以数据流（stream）的形式进行的。对于大文件，数据是一段一段得到**的。


## 二 使用
fetch挂载在window全局对象上，所以可以用以下代码检查浏览器是否部署了Fetch API：

```
if ("fetch" in window){
  // 支持
} else {
  // 不支持
}
```

**一个Fetch API进行请求的简单例子：**


```
fetch(url).then(function (response) {
  return response.json();
}).then(function (jsonData) {
  console.log(jsonData);
}).catch(function () {
  console.log('出错了');
});
```



上面代码向指定URL发请求，得到回应后将其转为JSON格式，输出到控制台。如出错，则输出一条提示信息。注意，**fetch方法返回的是一个Promise对象。**

## 三 其他细节

Fetch API引入三个新的对象（也是构造函数）：Headers, Request和Response。（Request对象和Response对象都有body属性，表示请求的内容。）


## 参考
### 已学习
[《JavaScript 标准参考教程（alpha）》，by 阮一峰](http://javascript.ruanyifeng.com/bom/ajax.html)

### 待学习

