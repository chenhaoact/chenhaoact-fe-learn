# webGL基础学习整理

## 一 简介

WebGL \(Web图形库\) 是一种JavaScript API，用于在任何兼容的Web浏览器中呈现交互式3D和2D图形；

WebGL通过引入一个与OpenGL ES 2.0紧密相符合的API，可以在HTML5 [`<canvas>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas)元素中使用；

内嵌在浏览器中，不需要相关插件，可多平台运行；

webgl1 基于OpenGL ES2.0（OpenGL ES2.0适用于嵌入式设备，因此也适用于移动终端）；

WebGL 2 是WebGL的一个主要更新，它通过WebGL2RenderingContext 接口提供。基于OpenGL ES 3.0，包含一些新功能。

### 1用途

#### （1）适用场景

### 2优缺点及对比

#### （1）优点

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
* Promoted extensions that are now core to WebGL 2: [Vertex Array objects](https://developer.mozilla.org/en-US/docs/Web/API/WebGLVertexArrayObject), [instancing](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/drawArraysInstanced), [multiple render targets](https://developer.mozilla.org/en-US/docs/Web/API/WebGL2RenderingContext/drawBuffers), [fragment depth](https://developer.mozilla.org/en-US/docs/Web/API/EXT_frag_depth)

另请参见博客文章 ["WebGL 2 lands in Firefox"](https://hacks.mozilla.org/2017/01/webgl-2-lands-in-firefox/) 和 [webglsamples.org/WebGL2Samples](http://webglsamples.org/WebGL2Samples/) 几个演示。

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

