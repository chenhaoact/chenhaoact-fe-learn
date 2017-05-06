# EasyAR引擎

## 一 简介

### 1用途

跨平台的 AR SDK。

3D 引擎支持：

Android/iOS GLES2

Unity 3D

未来更多（内嵌和外接）

### 2优缺点及对比

支持使用平面目标的AR，支持1000个以上本地目标的流畅加载和识别，支持基于硬解码的视频（包括透明视频和流媒体）的播放，支持二维码识别，支持多目标同时跟踪。

支持PC和移动设备等多个平台，EasyAR不会显示水印，也没有识别次数限制。

## 二 基本概念

## 三 使用及案例

按照官网注册创建应用后，到下载页面下载EasyAR SDK Unity Samples。

然后参考下列内容编译运行EasyAR的Unity样例：

[https://www.easyar.cn/view/docs/Getting-Started/Compile-and-Run-EasyAR-Unity-Samples.html](https://www.easyar.cn/view/docs/Getting-Started/Compile-and-Run-EasyAR-Unity-Samples.html)

或这里的视频（建议看视频更直观些）

http://v.youku.com/v\_show/id\_XMTQ5MDkxMDc5Ng==.html?from=s1.8-1-1.2



下载的EasyAR SDK Unity Samples里的readme里有样例的说明如下：

本包中包含EasyAR的Unity样例。

请阅读EasyAR网站上文档来了解应该如何来使用这些样例：[http://www.easyar.cn/view/documentapi.html](http://www.easyar.cn/view/documentapi.html)

样例:

HelloAR

* 演示如何创建第一个EasyAR应用

* 演示使用EasyAR在target上面显示3D内容和视频的最简单的方法

HelloARTarget

* 演示创建target的不同方法

* 演示如何动态创建target

HelloARVideo

* 演示如何使用EasyAR加载并在target上播放视频

* 演示本地视频播放

* 演示透明视频播放

* 演示流媒体视频播放

HelloARMultiTarget-SingleTracker

* 演示如何使用一个tracker同时跟踪多个目标

HelloARMultiTarget-MultiTracker

* 演示如何使用多个tracker同时跟踪多个目标

HelloARMultiTarget-SameImage

* 演示如何同时跟踪多个相同目标

HelloARQRCode

* 演示如何同时检测二维码并跟踪目标

TargetOnTheFly

* 演示如何直接从相机图像中实时创建target并load到tracker中

Coloring3D

* 演示如何创建“AR涂涂乐”，使绘图书中的图像实时“转换”成3D

图片Markers:

你可以在这些文件夹和其子文件夹中找到样例中使用的图片marker

* HelloAR/Assets/StreamingAssets

* HelloARTarget/Assets/StreamingAssets

* HelloARVideo/Assets/StreamingAssets

* HelloARMultiTarget-SingleTracker/Assets/StreamingAssets

* HelloARMultiTarget-MultiTracker/Assets/StreamingAssets

* HelloARMultiTarget-SameImage/Assets/StreamingAssets

* HelloARQRCode/Assets/StreamingAssets

* Coloring3D/Assets/StreamingAssets

所有这些marker（除了Coloring3D中的）都可以使用“视+”通过云识别来玩。这里面许多是有趣的AR游戏。

下载 视+ ，一起来玩吧！

```
http://www.sightp.com/

http://www.sightp.com/view/downloadapp.html
```



**我的案例运行：**

这里我运行了官方案例中第一个HelloAR里的ImageTarget-JsonFile-idback，点击unity里的运行：

![](/assets/importarcecccccccc.png)

然后把身份证正面对着摄像头，就会在身份证上出现一个立体的立方体。

第一个增强现实的例子就跑通了，此案例通过识别身份证图像来显示增强现实的物体影像。

## 四 资源

### 1官网

[https://www.easyar.cn/](https://www.easyar.cn/)

### 2文档（建议看下面我列的教程资源，因为官方文档实际写的较抽象，没有多少实例）

[https://www.easyar.cn/view/docs/Getting-Started/Getting-Started-with-EasyAR.html](https://www.easyar.cn/view/docs/Getting-Started/Getting-Started-with-EasyAR.html)

### 3源码

### 4教程

官方教程：

官网社区里的各种教程（推荐看）：

[http://bbs.sightp.com/forum-55-1.html](http://bbs.sightp.com/forum-55-1.html)

其他教程：

