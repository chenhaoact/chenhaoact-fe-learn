# location对象（url信息及路径控制（跳转，重载等））

**Location 对象包含有关当前 URL 的信息。
**

Location 对象是 Window 对象的一个部分，可通过 window.location 属性来访问。

document.location属性与window.location属性等价。IE曾不允许对document.location赋值，故**建议优先使用window.location**。

## window.location属性
返回location对象，提供了当前文档的URL信息**（比如网址参数等）**

```
// 当前网址为 http://user:passwd@www.example.com:4097/path/a.html?x=111#part1
window.location.href // "http://user:passwd@www.example.com:4097/path/a.html?x=111#part1"
window.location.protocol // "http:"
window.location.host // "www.example.com:4097"
window.location.hostname // "www.example.com"
window.location.port // "4097"
window.location.pathname // "/path/a.html"
window.location.search // "?x=111"
window.location.hash // "#part1"
window.location.user // "user"
window.location.password // "passwd"
```

## window.location对象的方法：

```
// 加载新的文档,跳转到另一个网址
window.location.assign('http://www.google.com')

// 优先从服务器重新加载
window.location.reload(true)

// 优先从本地缓存重新加载（默认值）
window.location.reload(false)

// 跳转到新网址，并将取代掉history对象中的当前记录
window.location.replace('http://www.google.com');

// 将location对象转为字符串，等价于window.location.href

window.location.toString()

```





