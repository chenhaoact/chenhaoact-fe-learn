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






## 二 归纳整理
### 字符串和数组都有（且使用类似）的方法整理：
concat

### 字符串没有数组才有的方法整理（重点！不要乱用）
join


## 参考
String常用方法（w3school）
http://www.w3school.com.cn/jsref/jsref_obj_string.asp




