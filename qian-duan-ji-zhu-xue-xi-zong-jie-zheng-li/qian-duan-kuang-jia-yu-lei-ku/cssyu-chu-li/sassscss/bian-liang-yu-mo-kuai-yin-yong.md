## 变量$
一般变量以$开头

### 特殊变量
一般我们定义的变量都为属性值，可直接使用，但是如果变量作为属性或在某些特殊情况下等则必须要以#{$variables}形式使用。

如果变量需要镶嵌在字符串之中，就必须需要写在#{}之中:


```
$borderDirection:       top !default; 
$baseFontSize:          12px !default;
$baseLineHeight:        1.5 !default;

//应用于class和属性
.border-#{$borderDirection}{
  border-#{$borderDirection}:1px solid #ccc;
}
//应用于复杂的属性值
body{
    font:#{$baseFontSize}/#{$baseLineHeight};
}

```

具体参考：
https://www.w3cplus.com/sassguide/syntax.html

## 模块引用  @import
将一个Sass 模板被切割为多个文件并通过 @import 引入。