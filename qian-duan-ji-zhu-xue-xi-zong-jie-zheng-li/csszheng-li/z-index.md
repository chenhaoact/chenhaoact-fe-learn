# 元素层叠显示优先级与z-index

## 元素层叠显示优先级
如果没有设置z-index则位置相同时后面的元素可以遮住前面的元素。

设置了z-index，值越大，则显示越靠上。

参考：
http://blog.leanote.com/post/codert/z-index%E5%B1%82%E5%8F%A0%E9%A1%BA%E5%BA%8F%E8%AF%A6%E8%A7%A3

## z-index无效问题
z-index只对定位元素有效，

就是设置了position属性的元素，position的属性值如下：absolute-绝对定位、relative-相对定位、fixed-固定定位、inherit-继承父元素定位，static-静态定位。

**注意，z-index并不是所有定位设置都有效，absolute、relative和fixed有效，inherit取决于父元素，如父元素没设置定位则z-index无效。**

**static**这个静态定位，是默认值，表示当前元素不进行定位，设置了这个值**z-index不起作用**。

另外：**z-index可以设置为负值**。


参考：
解决和分析CSS中z-index属性无效的问题
http://shiyousan.com/post/635861461562038949

## z-index最大值、最小值
不同类型及版本的浏览器不同，多数为-2147483648 到 2147483647 。

参考
z-index的最大值、最小值
http://www.cnblogs.com/shinnyChen/p/3758991.html