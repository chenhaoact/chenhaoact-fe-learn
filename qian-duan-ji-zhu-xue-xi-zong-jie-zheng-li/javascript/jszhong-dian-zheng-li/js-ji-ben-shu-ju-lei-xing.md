#js 基本数据类型及操作

1. 对象读一个不存在的属性返回 undefined

```
a={'a':1,'b':2}
a.data  //undefined
a.data || a.a //1
```

2. 对象读length也返回 undefined

```
a={'a':1,'b':2}
a.length  //undefined
```

3. **但 undefined 或 null 或 数字 读length就会跑出js异常 ！！！（避免页面有时因数据异常而白屏等故障尤其注意）**

```
undefined.length  //Uncaught TypeError: Cannot read property 'length' of undefined

null.length  //Uncaught TypeError: Cannot read property 'length' of null

1.length  //Uncaught SyntaxError: Invalid or unexpected token
```



