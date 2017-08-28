# URL的编码/解码及参数查询
## 一 URL的编码/解码方法

网页URL的合法字符分成两类。

URL元字符：分号（;），逗号（’,’），斜杠（/），问号（?），冒号（:），at（@），&，等号（=），加号（+），美元符号（$），井号（#）

语义字符：a-z，A-Z，0-9，连词号（-），下划线（_），点（.），感叹号（!），波浪线（~），星号（*），单引号（\），圆括号（()`）

除了以上字符，其他字符出现在URL之中都必须转义(**比如汉字**)，规则是根据操作系统的默认编码

JS提供四个URL的编码/解码方法。

### encodeURI()  decodeURI()

encodeURI() 参数是一个字符串，代表整个URL。它会将元字符和语义字符之外的字符，都进行转义。decodeURI用于还原转义后的URL。它是encodeURI的逆运算。

### encodeURIComponent() decodeURIComponent()

encodeURIComponent只转除了语义字符之外的字符，元字符也会被转义。因此，**它的参数通常是URL的路径或参数值，而不是整个URL**。

## 二 URL参数查询 URLSearchParams API
**URLSearchParams API用于处理URL之中的查询字符串，即问号之后的部分**。没有部署这个API的浏览器，可以用[url-search-params](https://github.com/WebReflection/url-search-params)这个垫片库。



```
var paramsString = 'q=URLUtils.searchParams&topic=api';
var searchParams = new URLSearchParams(paramsString);
```

URLSearchParams有以下方法，用来操作某个参数：

has()：返回一个布尔值，表示是否具有某个参数
get()：返回指定参数的第一个值
getAll()：返回一个数组，成员是指定参数的所有值
set()：设置指定参数
delete()：删除指定参数
append()：在查询字符串之中，追加一个键值对
toString()：返回整个查询字符串

## 参考
## 已学习
URL的编码/解码方法（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/bom/window.html#toc34

URLSearchParams API（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/bom/history.html#toc5

## 待学习


