# CSS画斜三角形和斜线

## 方法一：利用 CSS border（除了设置border外再设置两边上的border如border-right和border-bottom），可以轻松在div的一角实现一个三角形：

代码如下：

```
div{
  border:16px solid white;
  border-right:16px solid deeppink;
  border-bottom:16px solid deeppink;
}
```

上述代码会在div的左下角形成一个粉红色的三角（宽高为border线值的2倍，即32px）：

![](/assets/三角.png)



## 参考
### 待学习
有趣的CSS题目（9）：巧妙实现 CSS 斜线
http://web.jobbole.com/88927/