# js字符串

## 一 常用方法
### 1. concat() 连接两个或多个字符串后返回（原字符串不会变）
语法：


```
stringObject.concat(stringX,stringX,...,stringX)
```

例子


```
var str1="Hello "
var str2="world!"
document.write(str1.concat(str2)) // Hello world!  
// str1 还是 "Hello "
```

### 2. split() 把字符串（按特定分隔符）分割成字符串数组
语法

```
stringObject.split(separator,howmany)
```

例子


```
"2:3:4:5".split(":")	//将返回["2", "3", "4", "5"]
```

### 3. replace()  替换字符串中的子字符串（替换成''就相当于删除某自字符串）

语法

```
str.replace(regexp|substr, newSubStr|function)
```

**第一个参数是用于匹配被替换字符串的（正则或者自字符串）
第一个参数是替换为的新字符串（或生成它的函数）**

例子
```
var str = 'Twas the night before Xmas...';
var newstr = str.replace(/xmas/i, 'Christmas');
console.log(newstr);  // Twas the night before Christmas...
```

注意：原字符串不会改变。

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace

### 4. includes() 判断一个字符串是否包含在另一个字符串中

语法


```
str.includes(searchString[, position])
```

例子


```
'Blue Whale'.includes('blue'); // returns false
```

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/includes

### 5. substr 获取子字符串



```
stringObject.substr(start,length)
```

抽取从 start 下标开始的指定数目length的子字符串

参数：	
start	必需。要抽取的子串的起始下标。必须是数值。如果是负数，那么该参数声明从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。

length	可选。子串中的字符数。必须是数值。如果省略了该参数，那么返回从 stringObject 的开始位置到结尾的字串。

### 6. toUpperCase() toLowerCase() 转大写/小写

语法：



```
stringObject.toLowerCase()
```



**和 toLocaleUpperCase()与toLocaleLowerCase() 的对比 **
与 toLowerCase() 不同的是，toLocaleLowerCase() 方法按照本地方式把字符串转换为小写。只有几种语言（如土耳其语）具有地方特有的大小写映射，所有该方法的返回值通常与 toLowerCase() 一样。


## 二 归纳整理
### 1. 字符串和数组都有（且使用类似）的方法整理：
concat

### 2. 字符串没有数组才有的方法整理（重点！不要乱用）
join
强大的splice() 删除元素，并向数组添加新元素，字符串没有

### 3. 会改变原字符串的方法

### 4. 不会改变原字符串的方法
replace

### 5. 不要使用的方法

注意
**尽量不要用eval() 函数**

**eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码，非常危险！！！。虽然 eval() 功能非常强大，但实际使用中必须要用到它的情况并不多。**

比如：


```
eval('alert(\'hi\')')  //就能直接在浏览器中弹框提示hi
```

**eval()非常危险（特别是其参数会经过后端或用户返回时），项目中不要用。
**



## 参考
String常用方法（w3school）
http://www.w3school.com.cn/jsref/jsref_obj_string.asp




