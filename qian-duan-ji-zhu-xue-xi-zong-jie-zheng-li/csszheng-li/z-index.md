# z-index

## z-index无效问题
z-index只对定位元素有效，

就是设置了position属性的元素，position的属性值如下：absolute-绝对定位、relative-相对定位、fixed-固定定位、inherit-继承父元素定位，static-静态定位。

**注意，z-index并不是所有定位设置都有效，absolute、relative和fixed有效，inherit取决于父元素，如父元素没设置定位则z-index无效。**

**static**这个静态定位，是默认值，表示当前元素不进行定位，设置了这个值**z-index不起作用**。

另外：**z-index可以设置为负值**。


详细参考：
解决和分析CSS中z-index属性无效的问题
http://shiyousan.com/post/635861461562038949