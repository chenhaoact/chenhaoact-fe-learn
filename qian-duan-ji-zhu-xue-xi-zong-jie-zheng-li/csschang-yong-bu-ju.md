##居中

###垂直居中

如果要让div垂直居中的话，需要设置
position: absolute; 
//parent元素需要设置position:relative等;
top: 50%;
height: 30%; //或者其他值，或者定高都可以
margin-top: -15%; //margin-top取负的高度偏移回来只让top: 50%;起作用

具体参考： 
CSS 元素垂直居中的 6种方法
http://blog.csdn.net/wolinxuebin/article/details/7615098

##自适应

### web app使用rem代替px
**rem**是指**相对于根元素的字体大小的单位**。简单的说它就是一个相对单位。看到rem大家一定会想起em单位，**em**是**相对于父元素的字体大小的单位**。它们之间其实很相似，只不过一个计算的规则是依赖根元素一个是依赖父元素计算。

https://isux.tencent.com/web-app-rem.html