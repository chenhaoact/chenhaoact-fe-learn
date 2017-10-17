#js 基本数据类型及操作

## 数据类型判断
### typeof （常用）
typeof操作符返回一个字符串，指示未经计算的数据类型。



```
typeof operand

```


参数
operand 是一个表达式，表示对象或原始值，其类型将被返回。

可能的返回值：

| 类型 | 结果 |
| -- | -- |
| Undefined |	"undefined" |
| Null | "object" |
| Boolean | "boolean" |
| Number | "number" |
| String | "string" |
| Symbol (ECMAScript 6 新增) |	"symbol" |
| 宿主对象(由JS环境提供) |	Implementation-dependent|
| **函数对象 "function"** | 任何其他对象	"object"|

使用：
比如**在react中调用组件传过来的回调函数时需要先判断所传数据是否为函数类型**：



```
const callback = this.props;

if(typeOf callback === 'function'){
   callback && callback()
}
```

**在进行特定的数据操作前，务必检查下数据的类型是否正确，避免因数据类型不正确二导致的js报错，异常甚至故障。**


## 数据类型操作
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
4. **注意！undefined 或 null 读任何它没有的属性都会报错（避免页面有时因数据异常而白屏等故障尤其注意）**

```
res.data.data.list  //当res.data里没有data的时候相当于是读 undefined.list 就会抛出js异常导致页面不正常
```

所以建议数据有这种可能性的情况下**做个兼容(先判断要读取某属性的变量是否为空在去读取其属性)**：

```
if(res.data.data){
   res.data.data.list
} else {
   res.data.list
}

```

## 相等的判断



```
undefined == null //true
'' == null //false
```



## 数据类型转化


### 字符串转数字


转为整数(parseInt只截取整数部分，不四舍五入)
```
parseInt('1.1')  //1
parseInt('1')  //1
```

保留小数：
```
parseFloat('1.1')  //1.1
parseFloat('1')  //1

```

如果字符串的第一个字符不能被转换为数字，那么会返回NaN。

**强制类型转换(建议使用)**
还可使用强制类型转换（type casting）处理转换值的类型。使用强制类型转换可以访问特定的值，即使它是另一种类型的。

**ECMAScript中可用的3种强制类型转换如下：
Boolean(value)——把给定的值转换成Boolean型；
Number(value)——把给定的值转换成数字（可以是整数或浮点数）；
String(value)——把给定的值转换成字符串。**


Number()的强制类型转换与parseInt()和parseFloat()方法的处理方式相似，只是它转换的是整个值，而不是部分值。

**数字取整**
floor() 方法执行的是向下取整计算，它返回的是小于或等于函数参数，并且与之最接近的整数。 （记忆方法：floor是地板）

ceil() 方法执行的是向上取整计算，它返回的是大于或等于函数参数，并且与之最接近的整数。


## 表达式



```
null ? 'a' : 'b' //b

undefined ? 'a' : 'b' //b


0 ? 'a' : 'b' //b   注意！！！


'a' ? 'a' : 'b' //a
2 ? 'a' : 'b' //a  
[] ? 'a' : 'b' //a  
```





