## 一 数字类型的数据需要注意的问题
### 1. JavaScript 浮点数运算的精度问题（重要！）
JavaScript 中整数和浮点数都属于 Number 数据类型，所有数字都是以 64 位浮点数形式储存，即便整数也是如此。 

**在一些特殊的数值表示与计算中，例如金额（和钱相关的开发点都应该高度重视！），js 的 Number的就可能出问题。**

比如： **1.01*100 就可能出现和显示 101.0000000000001 **

所以**金额等精度很重要的数据的加减乘除，以及小数的运算都不要直接使用js的 + - * / ，而要单独使用一套方法（以字符串的方式进行处理），具体参考下文**：

JavaScript 浮点数运算的精度问题
http://www.css88.com/archives/7340



## 二 数字类型数据常用方法
### 1. 取整 
**Math.ceil() === 向上取整**

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil


**Math.floor() === 向下取整**

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/floor

### 2. 浮点数转整数  parseInt()

parseInt(string, radix)

参数
string	必需。要被解析的字符串。
radix	可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。

例子


```
parseInt("10");			//返回 10
parseInt("19",10);		//返回 19 (10+9)
parseInt("11",2);		//返回 3 (2+1)
parseInt("17",8);		//返回 15 (8+7)
parseInt("1f",16);		//返回 31 (16+15)
parseInt("010");		//未定：返回 10 或 8
```




### NaN
使用Number()可以将数据转为数字类型，如果转不了，则会返回NaN。

因为NaN 不等于 NaN，所以不要使用 == 判断是否为 NaN，要用isNaN判断。

用以下写法判断能否转为数字类型：

```
let a = 'a';
isNaN(Number(a))  // false
```

### 判断小数点后有几位


```
3.66.toString().split('.')[1].length  // 2
```








