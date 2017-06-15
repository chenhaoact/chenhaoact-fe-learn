# svg

## 一 简介

### 1用途

**使用 XML 来描述二维图形和绘图程序的语言。**

定义用于网络的可伸缩矢量图形

### 2优缺点及对比

一般的图像（如BMP,PNG,JPG等）是位图，是基于颜色的描述，规则图形的像素点

而矢量图（SVG,AI等）是基于数学的描述（各个曲线是什么曲线，参数是什么，用什么颜色填充等）

与其他图像格式相比，使用 SVG 的优势在于：

* SVG 可被非常多的工具读取和修改（比如记事本）
* SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
* SVG 是可伸缩的
* SVG 图像可在任何的分辨率下被高质量地打印
* SVG 可在图像质量不下降的情况下被放大
* SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
* SVG 可以与 Java 技术一起运行
* SVG 是开放的标准
* SVG 文件是纯粹的 XML

SVG 的主要竞争者是 Flash。

与 Flash 相比，SVG 最大的优势是与其他标准（比如 XSL 和 DOM）相兼容。而 Flash 则是未开源的私有技术。

## 二 基本概念与技术重点整理

### 1 SVG使用方式（四种）

浏览器直接打开

在HTML中使用&lt;img&gt;标签引用

直接在HTML中使用SVG标签

作为CSS背景



### 2 SVG 形状

SVG 有一些预定义的形状元素：

#### （1）矩形 &lt;rect&gt;

 width 和 height 属性可定义矩形的高度和宽度

x和y属性定义左上角定点的坐标

rx和ry属性定义矩形圆角

style 属性用来定义 CSS 属性：

CSS 的 fill 属性定义矩形的填充颜色（rgb 值、颜色名或者十六进制值）

CSS 的 stroke-width 属性定义矩形边框的宽度

CSS 的 stroke 属性定义矩形边框的颜色

#### （2）圆形 &lt;circle&gt;

cx和cy属性： 圆心坐标

r属性： 半径



#### （3）椭圆 &lt;ellipse&gt;





* 线 &lt;line&gt;



* 折线 &lt;polyline&gt;



* 多边形 &lt;polygon&gt;



* 路径 &lt;path&gt; 可绘制任意图形，如各种曲线



### 

## 三 使用实践及案例

## 四 资源

### 1官网

w3c指定的svg标准（1.1）

[https://www.w3.org/TR/SVG11/](https://www.w3.org/TR/SVG11/)

### 2文档

### 3源码

### 4教程

官方教程：

其他教程：

w3school的svg教程

[http://www.w3school.com.cn/svg/](http://www.w3school.com.cn/svg/)

慕课网视频教程-走进SVG

[http://www.imooc.com/learn/143](http://www.imooc.com/learn/143)

w3cplus（svg专题）

[https://www.w3cplus.com/blog/tags/411.html](https://www.w3cplus.com/blog/tags/411.html)

### 5工具与资源

svg的浏览器支持情况（目前大多数主流版本的浏览器都支持svg）

[http://caniuse.com/\#search=svg](http://caniuse.com/#search=svg)

