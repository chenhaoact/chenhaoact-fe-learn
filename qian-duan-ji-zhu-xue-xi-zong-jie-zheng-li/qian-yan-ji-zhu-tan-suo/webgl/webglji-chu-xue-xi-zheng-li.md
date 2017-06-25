# webGL基础学习整理

## 一 简介

WebGL \(Web图形库\) 是一种JavaScript API，用于在任何兼容的Web浏览器中呈现交互式3D和2D图形；

WebGL通过引入一个与OpenGL ES 2.0紧密相符合的API，可以在HTML5 [`<canvas>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas)元素中使用；

内嵌在浏览器中，不需要相关插件，可多平台运行；

webgl1 基于OpenGL ES2.0（OpenGL ES2.0适用于嵌入式设备，因此也适用于移动终端）；

WebGL 2 是WebGL的一个主要更新，它通过WebGL2RenderingContext 接口提供。基于OpenGL ES 3.0，包含一些新功能。

### 1用途

#### （1）适用场景



### 2优缺点及对比

#### （1）优点

基于web实现3D效果，能快速传播，跨平台，无需插件

介入了设备底层的硬件加速，速度较快

#### （2）缺点

## 二 基本概念与技术重点整理

### \(2\)WebGL 2

WebGL 2 是WebGL的一个主要更新，它通过WebGL2RenderingContext 接口提供。它基于OpenGL ES 3.0，新功能包括：

* [3D textures](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/texImage3D)
* [Sampler objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLSampler)
* [Uniform Buffer objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext#Uniform_buffer_objects)
* [Sync objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLSync)
* [Query objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLQuery)
* [Tranform Feedback objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLTransformFeedback)
* Promoted extensions that are now core to WebGL 2: [Vertex Array objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLVertexArrayObject), [instancing](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/drawArraysInstanced), [multiple render targets](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/drawBuffers), [fragment depth](https://developer.mozilla.org/en-US/docs/Web/API/EXT_frag_depth)

另请参见博客文章 ["WebGL 2 lands in Firefox"](https://hacks.mozilla.org/2017/01/webgl-2-lands-in-firefox/) 和 [webglsamples.org/WebGL2Samples](http://webglsamples.org/WebGL2Samples/) 几个演示。



### \(13\)图形api的实时模式与保留模式

在图像渲染领域，存在“实时模式”\(immediate mode\)和“保留模式”\(retained mode\)的区别。**HTML5 Canvas以及webGL属于实时模式 — 每次当图像发生改变时，Canvas中所有的元素都需要重画**。这种模式有一定的好处；比如，使用全局属性可以让滤镜效果的实现变得非常容易。一旦掌握了实时模式的运用，在Canvas上绘图就是一件很简单的事情 — 当图像有任何更新的时候，直接重画整个Canvas即可。**相比于保留模式，实时模式更灵活，但代码会多一些。**

与此相反，在保留模式下，绘图板保存了绘制对象的集合，并通过显示列表\(Display List\)对这些对象进行操作。**Flash和Silverlight都是在保留模式下工作的**。对于一个应用程序，如果它需要多个记录自己状态的对象的话，保留模式非常有用。而对于充分利用Canvas特性的HTML5应用程序（游戏、动画等）来说，使用一张类似保留模式下的绘图板来保存绘制对象，将会让工作变得更加简单。

因此，如何在利用实时模式的好处的同时，加入保留模式开发方式的支持，是一个比较有趣的挑战。

## 三 使用实践及案例

## 四 资源与参考

### 1官网

### 2文档

### 3源码

### 4教程

#### （1）已学习：

#### （2）学习中：

极客学院webgl教学视频  
[http://search.jikexueyuan.com/course/?q=webgl](http://search.jikexueyuan.com/course/?q=webgl)

#### （3）待学习：

官方教程：

其他教程：  
mozilla开发者官网的webgl文档（推荐的webgl api参考）  
[https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL\_API](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API)

极客学院wiki-WebGL中文版  
[http://wiki.jikexueyuan.com/project/webgl/](http://wiki.jikexueyuan.com/project/webgl/)

khronos的webgl wiki  
[https://www.khronos.org/webgl/wiki/](https://www.khronos.org/webgl/wiki/)

### 5工具与资源

opengl官网  
[https://www.opengl.org/](https://www.opengl.org/)

