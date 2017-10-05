# Ajax
## 一 简介
**AJAX：js脚本发起HTTP通信。通过原生的XMLHttpRequest对象发出HTTP请求，得到服务器返回的数据后，再进行处理。**

AJAX可以是同步请求，也可是异步请求。但大多数情况特指异步请求。因为同步的Ajax请求对浏览器有“堵塞效应”。

## 二 XMLHttpRequest对象
XMLHttpRequest对象用来在浏览器与服务器之间传送数据。

```
var ajax = new XMLHttpRequest();
ajax.open('GET', 'http://www.example.com/page.php', true);
```

上面代码向指定服务器网址发GET请求。

然后，AJAX指定回调函数，监听通信状态（readyState属性）变化。


```
ajax.onreadystatechange = handleStateChange;
```

**一旦拿到服务器返回数据，AJAX不会刷新整个网页，而是只更新相关部分，从而不打断用户正在做的事情。**

**AJAX只能向同源网址（协议、域名、端口都相同）发**HTTP请求，如果发跨源请求会报错。

XMLHttpRequest可以报送各种数据，包括字符串和二进制，除了HTTP，它还支持通过其他协议传送（如File和FTP）。

**XMLHttpRequest对象的典型用法：
**


```
var xhr = new XMLHttpRequest();

// 指定通信过程中状态改变时的回调函数
xhr.onreadystatechange = function(){
  // 通信成功时，状态值为4
  if (xhr.readyState === 4){
    if (xhr.status === 200){
      console.log(xhr.responseText);
    } else {
      console.error(xhr.statusText);
    }
  }
};

xhr.onerror = function (e) {
  console.error(xhr.statusText);
};

// open方式用于指定HTTP动词、请求的网址、是否异步
xhr.open('GET', '/endpoint', true);

// 发送HTTP请求
xhr.send(null);

```

open方法的第三个参数是布尔值，表示是否为异步请求。

## 三 XMLHttpRequest实例的属性
1. readyState： 
XMLHttpRequest请求当前所处的状态

2. **response： 
返回接收到的数据体（即body部分）**。它的类型可以是ArrayBuffer、Blob、Document、JSON对象、或者一个字符串，这由XMLHttpRequest.responseType属性的值决定。如果本次请求没有成功或者数据不完整，该属性就会等于null。

3. responseType：
指定服务器返回数据（xhr.response）的类型。

4. **status：
本次请求所得到的HTTP状态码**，它是一个整数。一般来说，如果通信成功状态码是200。
**200, 访问正常**
301, 永久移动
302,暂时移动
**304,未修改**
307,暂时重定向
401, 未授权
403, 禁止访问
**404, Not Found，未发现指定网址**
**500，服务器发生错误**
基本上，只有**2xx和304的状态码，表示服务器返回正常**。

5. withCredentials：
（布尔值）表示**跨域请求时，用户信息（如Cookie和认证的HTTP头信息）是否会包含在请求中，默认false**。

如果需要通过跨域AJAX发送Cookie，需要将withCredentials设为true;

为了让这个属性生效，服务器必须显式返回Access-Control-Allow-Credentials这个头信息：

Access-Control-Allow-Credentials: true

## 参考
### 已学习
[《JavaScript 标准参考教程（alpha）》，by 阮一峰](http://javascript.ruanyifeng.com/bom/ajax.html)

### 待学习

