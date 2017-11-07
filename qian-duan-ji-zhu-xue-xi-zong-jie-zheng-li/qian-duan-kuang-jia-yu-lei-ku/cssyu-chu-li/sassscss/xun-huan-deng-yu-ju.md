## 循环
for循环有两种形式，分别为：


```
@for $var from through 
```



和



```
@for $var from to
```



$i表示变量，start表示起始值，end表示结束值，这两个的区别是**关键字through表示包括end这个数，而to则不包括**end这个数。

例子：


```
@for $var from through 64{
  .font-size-#{$i}{
    font-size: $i * 1px !important;
  }
}
```

使用 font-size-16样式类即可设置font-size为16px，减少了css代码的重复书写，提升代码复用率。


## 参考
sass揭秘之@if，@for，@each
https://www.w3cplus.com/preprocessor/sass-advanced-application.html

Sass的控制命令（循环）
http://www.cnblogs.com/alice-shan/p/4971829.html