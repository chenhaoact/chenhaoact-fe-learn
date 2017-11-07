# Sass函数
## 一 内置函数
有很多Sass内置的较强大的函数可以直接使用。


Sass基础——Sass函数
https://www.w3cplus.com/preprocessor/sass-other-function.html

## 二 自定义函数
SASS允许用户编写自己的函数。

```
　　@function double($n) {
　　　　@return $n * 2;
　　}
　　#sidebar {
　　　　width: double(5px);
　　}
```


