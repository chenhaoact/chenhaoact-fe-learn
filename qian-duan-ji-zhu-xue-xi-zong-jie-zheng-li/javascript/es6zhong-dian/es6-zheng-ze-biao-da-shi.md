# ES6 RegExp（正则表达式）包括ES5部分

## 一 简介

### 1. 什么是正则表达式？

**正则表达式是用于匹配字符串中字符组合的**模式。在JS中，正则表达式也是对象。

### 2. 正则表达式的用途

正则表达式可被用于[`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)的 [`exec`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec)和 [`test`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)方法, 以及 [`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)的 [`match`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match)、[`replace`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)、[`search`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search)和 [`split`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)方法。

### 3. 正则表达式的创建

### 方法1使用一个正则表达式字面量，其由包含在斜杠之间的模式组成：

```
/*
   /pattern/flags 
*/

const regex = /ab+c/;

const regex = /^[a-zA-Z]+[0-9]*\W?_$/gi;
```

在加载脚本后，正则表达式字面值提供正则表达式的编译。**当正则表达式不变时，使用此方法可获得更好的性能**。

### 方法2 调用RegExp对象的构造函数：

```
/* 
    new RegExp(pattern [, flags])
*/
```

### 4. 匹配模式的特殊字符（pattern，放置在/ /之间）

| 匹配字符 | 作用 |
| :--- | :--- |
| \ | 加在非特殊字符前，表示下一个字符是特殊字符；加在特殊字符前，将其**转义**为字面量 |
| ^ | 匹配输入的开头 |
| $ | 匹配输入的结束 |
| \* | 匹配前一个表达式0次或多次，等价于 {0,}。 |
| + | 匹配前面一个表达式1次或者多次。等价于 {1,} |
| ? | 匹配前面一个表达式0次或者1次。等价于 {0,1}。 |
| . | （小数点）匹配除换行符之外的任何单个字符 |
| \(x\) | 匹配 'x' 并且记住匹配项 |
| \(?:x\) | 匹配 'x' 但是不记住匹配项 |
| x\(?=y\) | 匹配'x'仅仅当'x'后面跟着'y' |
| x\(?!y\) | 匹配'x'仅仅当'x'后面不跟着'y' |
| \`x | y\` | 匹配‘x’或者‘y’ |
| {n} | 匹配了前面一个字符刚好发生了n次 |
| {n,m} | 匹配前面的字符至少n次，最多m次 |
| \[xyz\] | 一个字符集合。匹配方括号的中任意字符，包括转义序列。你可以使用破折号（-）来指定一个字符范围。 |
| ^\[xyz\] | 一个反向字符集。匹配任何没有包含在方括号中的字符。可使用破折号（-）来指定一个字符范围 |
| \d | 匹配一个数字,等价于\[0-9\] |
| \D | 匹配一个非数字字符,等价于[^0-9] |

例如：  
/^A/ 并不会匹配 "an A" 中的 'A'，但是会匹配 "An E" 中的 'A'；

/t$/ 并不会匹配 "eater" 中的 't'，但是会匹配 "eat" 中的 't'。

/bo\*/会匹配 "A ghost boooooed" 中的 'booooo' 和 "A bird warbled" 中的 'b'

/a+/匹配了在 "candy" 中的 'a'，和在 "caaaaaaandy" 中所有的 'a'。

/e?le?/ 匹配 "angel" 中的 'el'，和 "angle" 中的 'le' 以及"oslo' 中的'l'



### 5. 正则的使用

正则表达式可以被用于[`RegExp`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp)的[`exec`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp/exec)和[`test`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp/test)方法以及 [`String`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String)的[`match`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/match)、[`replace`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/replace)、[`search`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/search)和[`split`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/split)方法。这些方法在[JavaScript 手册](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference)中有详细的解释。

|  |  |
| :--- | :--- |
| 方法 | 描述 |
| [`exec`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp/exec) | 在字符串中执行**查找匹配**（**RegExp的方法**），返回一数组（未匹配到则返null） |
| [`test`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/RegExp/test) | 在字符串中测试**是否匹配**（RegExp的方法），返回true或false |
| [`match`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/match) | 在字符串中执行**查找匹配**（**String的方法**），返回一个数组或在未匹配到时返null |
| [`search`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/search) | 在字符串中测试匹配（String的方法），**返回匹配到的位置索引**，或者在失败时返回-1 |
| [`replace`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/replace) | 在字符串中执行查找匹配（String的方法），并使用替换字符串**替换**掉匹配到的子字符串 |
| [`split`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/String/split) | 用正则表达式或一个固定字符串**分隔**一个字符串，并将分隔后子字符串存储到数组中（String的方法） |

####附：平时开发中用过的正则表达式收集

1. input或textarea中的输入字符串.replace(/\n/g, '\\n').replace(/\t/g, '\\t')   
用正则表达式将文本中的空格和换行替换成 \t和\n  ，方便后端识别和解析 

2. 

### 6. ES6正则的扩展   TODO???

## 参考

### 已学习

[js正则表达式\(MDN\)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

### 待学习

[正则的扩展\(阮一峰《ES6标准入门》\)](http://es6.ruanyifeng.com/#docs/regex)

