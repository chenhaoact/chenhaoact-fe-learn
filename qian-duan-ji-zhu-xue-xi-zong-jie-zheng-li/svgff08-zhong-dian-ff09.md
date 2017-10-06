# svg

## 一 简介

### 1用途

**使用 XML 来描述二维图形和绘图程序的语言。**

定义用于网络的**可伸缩矢量图形**

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

cx 属性定义圆点的 x 坐标

cy 属性定义圆点的 y 坐标

rx 属性定义水平半径

ry 属性定义垂直半径

#### （4）线 &lt;line&gt;

x1 属性：线条的结束点的x坐标

y1 属性：线条的结束点的y坐标

x2 属性：线条的结束点的x坐标

y2 属性：线条的结束点的y坐标

#### （5）折线 &lt;polyline&gt;

折线每个端点的 x 和 y 坐标

#### （6）多边形 &lt;polygon&gt;

points 属性：多边形每个角的 x 和 y 坐标

#### （7）路径 &lt;path&gt; ，可绘制任意图形，如各种曲线

下面的命令可用于路径数据，写在path的d属性中：

* M = moveto
* L = lineto
* H = horizontal lineto
* V = vertical lineto
* C = curveto
* S = smooth curveto
* Q = quadratic Belzier curve
* T = smooth quadratic Belzier curveto
* A = elliptical Arc
* Z = closepath

注释：以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位。

### 3 svg图形的样式属性

fill 填充颜色

stroke 描边颜色

stroke-width 描边宽度

transform 坐标与父坐标系相比的变换值。如旋转角度等。

### 4 js对svg进行操作的基本api

#### （1）创建图形\(不是createElement，因为svg有自己的namespace\)

document.createElementNS\(ns,tagName\)

#### （2）添加图形

element.appendChild\(childElement\)

#### （3）设置/获取属性

element.setAttribute\(name,value\)

element.getAttribute\(name\)

### 5 SVG坐标系统

#### （1）视窗

`<svg>`元素上使用`width`和`height`声明视窗尺寸，也就是svg元素的内容尺寸。（不带单位默认是px）

初始**视窗坐标系**是一个建立在视窗上的坐标系。原点`(0,0)`在视窗的左上角，`X`轴正向指向右，`Y`

轴正向指向下。

#### （2）视野：viewBox，preserveAspectRatio

`viewBox`属性：声明用户坐标系（即用户所看到的坐标系），viewBox区域变大，则看到的视野变大，但所看到的形状会显得变小。（）

`preserveAspectRatio`属性：如果用不同于视窗的宽高比定义用户坐标系，就需要用`preserveAspectRatio`属性强制统一缩放比来保持图形的宽高比。

具体参考：

理解SVG坐标系和变换（第一部分）-viewport，viewBox，和preserveAspectRatio

[http://www.w3cplus.com/html5/svg-coordinate-systems.html](http://www.w3cplus.com/html5/svg-coordinate-systems.html)

#### （3）svg坐标系统

**x轴朝右，y轴朝下，旋转正角度是顺时针。**



#### （4）图形分组与引用

`<g>`标签创建分组（分组可以嵌套）。

使用&lt;use&gt;重用现有的元素。



具体参考：

SVG中的结构化、分组和引用元素

http://www.w3cplus.com/svg/structuring-grouping-referencing-in-svg.html



#### （5）坐标变换 transform

transform属性定义坐标变换。

常见如：平移，旋转, 缩放, 倾斜等。


##### 1）平移`translate(）`



```
<circle cx="0" cy="0" r="100" transform="translate(100 300)"/>
```


上面的代码将一个元素向x坐标轴方向（下）移动100个用户单位，向y坐标轴方向（右）移动300个用户单位。


##### 2）旋转`rotate()`

```
<g id="parrot" transform="rotate(45 50 50)" x="0" y="0"> <!-- elements making up a parrot shape --> </g>
```
上面的代码以当前用户坐标系中的(50,50)点为中心将一组元素进行45°旋转。


##### 3）缩放`scale()`



```
<rect width="150" height="100" transform="scale(2 0.5)" x="0" y="0" />
```

上面的代码把一个元素缩放到最初宽度的两倍，并且把高度压缩到最初的一半。



##### 4）倾斜 skewX()和skewY()



```
skewX(<skew-angle>)
skewY(<skew-angle>)

```


函数skewX声明一个沿x轴的倾斜；函数skewY声明一个沿y轴的倾斜。




坐标变换transform具体参考：

理解SVG坐标系统和变换： transform属性

https://www.w3cplus.com/html5/svg-transformations.html

#### 

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
mozilla开发者中心SVG专题

[https://developer.mozilla.org/zh-CN/docs/Web/SVG](https://developer.mozilla.org/zh-CN/docs/Web/SVG)

mozilla开发者中心SVG教程

[https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial)

w3school的svg教程

[http://www.w3school.com.cn/svg/](http://www.w3school.com.cn/svg/)

慕课网视频教程-走进SVG

[http://www.imooc.com/learn/143](http://www.imooc.com/learn/143)

w3cplus（svg专题）

[https://www.w3cplus.com/blog/tags/411.html](https://www.w3cplus.com/blog/tags/411.html)

### 5工具与资源

svg的浏览器支持情况（目前大多数主流版本的浏览器都支持svg）

[http://caniuse.com/\#search=svg](http://caniuse.com/#search=svg)

svg相关元素的清单及作用

[https://developer.mozilla.org/en-US/docs/Web/SVG/Element      
](/h ttps://developer.mozilla.org/en-US/docs/Web/SVG/Element)

[http://www.w3school.com.cn/svg/svg\_reference.asp](http://www.w3school.com.cn/svg/svg_reference.asp)

SVG DOM接口列表  
[https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model\#SVG\_interfaces](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model#SVG_interfaces)

