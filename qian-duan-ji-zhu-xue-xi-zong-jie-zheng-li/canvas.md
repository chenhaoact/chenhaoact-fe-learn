# canvas

## 一 简介

### 1用途

canvas简单的来说，就是html5提供的画布，可以通过它绘制各种各样的图，2d的，3d的都可以，可以自由的发挥创造力进行任意图像，动画的绘制。

### 2优缺点及对比

## 二 基本概念与技术重点整理

所有的代码整理在：[https://github.com/chenhaoact/Front-End-Learn/tree/master/CanvasLearn](https://github.com/chenhaoact/Front-End-Learn/tree/master/CanvasLearn)

### 1`<canvas>`元素

```
<canvas id="tutorial" width="150" height="150"></canvas>
```

通常会配上id，宽高不建议使用css定义，应使用width和height属性，不要带单位（会同时指定画布内部的元素宽高）。可以使用html标签的常见style属性设置位置等样式。

### 2渲染上下文

[`<canvas>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas) 元素创造了一个固定大小的画布，它公开了一个或多个**渲染上下文**，可用来绘制和处理要展示的内容。这里主要先介绍2D渲染上下文中。其他种类的上下文也许提供了不同种类的渲染方式；如，[**WebGL**](https://developer.mozilla.org/en-US/docs/Web/WebGL)**使用了基于**[**OpenGL ES**](http://www.khronos.org/opengles/)**的3D上下文 \("experimental-webgl"\) 。**

canvas起初是空白的。**为了展示，首先需要用脚本找到渲染上下文，然后在它的上面绘制**。[`<canvas>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas)** 元素有一个叫做 **[`getContext()`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement/getContext)`的方法，这个方法是用来`**获得渲染上下文和它的绘画功能**。`getContext()`只有一个参数，上下文的格式。对于2D图像而言，可以用[`CanvasRenderingContext2D`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D)。

```
var canvas = document.getElementById('tutorial');
var ctx = canvas.getContext('2d');
```

### 3.画直线

`beginPath()`

新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。

`closePath()`

闭合路径之后图形绘制命令又重新指向到上下文中。

`stroke()`

通过线条来绘制图形轮廓。

`fill()`

通过填充路径的内容区域生成实心的图形。  
`moveTo(`_`x`_`,`_`y`_`)`

将笔触移动到指定的坐标x以及y上。

[`lineTo(x, y)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/lineTo)

绘制一条从当前位置到指定x以及y位置的直线。

参考

https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas\_API/Tutorial/Drawing\_shapes\#绘制矩形

https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas\_API/Tutorial/Drawing\_shapes\#绘制路径

https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas\_API/Tutorial/Drawing\_shapes\#绘制一个三角形

### 4.绘制圆与弧

[`arc(x, y, radius, startAngle, endAngle, anticlockwise)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/arc)

画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。

[`arcTo(x1, y1, x2, y2, radius)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/arcTo)

根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点。

参考

https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas\_API/Tutorial/Drawing\_shapes\#圆弧

### 5.清空某区域
context.clearRect(x,y,width,height) 可以对画布上指定的矩形区域进行一次清空

### 6 得到画布对象
context.canvas 可以得到画布对象，从而调用画布对象的属性和方法。

## 

## 三 使用实践及案例

1 代码在project/front/FrontEndLearn/CanvasLearn下的

## 四 资源

### 1官网

### 2文档

### 3源码

### 4教程

#### （1）已学习：

慕课网视频教程-炫丽的倒计时效果Canvas绘图与动画基础

[http://www.imooc.com/learn/133](http://www.imooc.com/learn/133)

#### （2）学习中：

慕课网视频教程-Canvas绘图详解

[http://www.imooc.com/learn/185](http://www.imooc.com/learn/185)


#### （3）待学习：
官方教程：

其他教程：



Canvas教程\(mozilla开发者官网\)

[https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas\_API/Tutorial](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)

Canvas学习系列教程（大漠）

[https://www.w3cplus.com/canvas/introduction-to-prepare.html](https://www.w3cplus.com/canvas/introduction-to-prepare.html)

[https://www.w3cplus.com/blog/tags/616.html](https://www.w3cplus.com/blog/tags/616.html)

慕课网视频教程-Canvas玩转图像处理

[http://www.imooc.com/learn/476](http://www.imooc.com/learn/476)

学写一个字（介绍canvas如何与鼠标、触控交互）

[http://www.imooc.com/learn/284](http://www.imooc.com/learn/284)

极客学院Canvas相关视频教程

[http://search.jikexueyuan.com/course/?q=canvas](http://search.jikexueyuan.com/course/?q=canvas)

### 5工具与资源



