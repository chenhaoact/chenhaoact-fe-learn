# html5重点与新特性整理

## 一 简介

### 1用途

### 2优缺点及对比

## 二 基本概念与技术重点整理

### （1）html5标签大全
**html4原有的元素(此处只列出常用元素，全部元素列表（包括h5）见http://www.runoob.com/tags/ref-byfunc.html) 和 HTML 元素速查列表：http://www.runoob.com/html/html-quicklist.html：**

|元素|用途|
|:--|:--|
|<**h1**> - <**h6**>|标题，<**h1**>最大，<**h6**>最小(浏览器会自动地在标题的前后添加空行)|
|<**hr**>|水平线|
|<**p**>|段落|
|<**br**> （单标签）|换行|
|<**b**>或<**strong**>|粗体字|
|<**i**>或<**em**>|斜体字|
|<**code**>|定义计算机代码|
|<**a**>|链接|
|<**img**>|图像|
|<**table**>|定义表格|
|<**tr**>|表格的行|
|<**td**>|每行的各个单元格|
|<**th**>|表格的表头,表头<**tr**>中代替<**td**>|
|<**ul**>|无序列表是一个项目的列表，此列项目使用粗体圆点进行标记|
|<**ol**>|有序列表，列表项目前面使用数字进行标记|
|<**li**>|列表的每一项|
|<**dl**>|自定义列表,不仅仅是一列项目，而是项目及其注释的组合。自定义列表项以 <dt> 开始,替换li中的点和ol里的数字序号,列表项的定义以 <dd> 开始。|
|<**div**>|定义了文档的区域，块级|
|<**span**>|用来组合文档中的行内元素，内联元素(inline)|
|<**form**>|表单|
|<**input**>|输入标签|
|<**iframe**>|框架，以便在同一个浏览器窗口中显示不止一个页面，可用作公共页面部分的共用|
|<**script**>|定义了客户端js脚本|


**html5新增的元素：**

HTML5添加了很多新元素及功能，比如: 图形的绘制，多媒体内容，更好的页面结构，更好的形式处理，和几个api拖放元素，定位，包括网页应用程序缓存，存储，网络工作者等。

|元素|用途|
|:--|:--|
|**1 canvas新元素**||
|<**canvas**>|画布，标签定义图形，比如图表和其他图像，可以使用 JavaScript 在网页上绘制图像|
|**2 新多媒体元素：**||
|<**audio**>|音频|
|<**video**>|视频|
|<**source**>|定义多媒体资源 <**video**> 和 <**audio**>|
|<**embed**>|定义嵌入的内容，比如插件|
|<**track**>|诸如 <**video**> 和 <**audio**> 元素之类的媒介规定外部文本轨道,即：字幕|
|**3 新表单元素：**||
|<**datalist**>|定义选项列表,与 input 元素配合使用|
|<**keygen**>|规定用于表单的密钥对生成器字段|
|<**output**>|定义不同类型的输出，比如脚本的输出|
|**4 新的语义和结构元素：**|**（用来创建更好的页面结构）**|
|<**article**>|定义页面独立的内容区域|
|<**aside**>|定义页面的侧边栏内容|
|<**bdi**>|允许设置一段文本，使其脱离其父元素的文本方向设置|
|<**command**>|定义命令按钮，比如单选按钮、复选框或按钮|
|<**details**>|描述文档或文档某个部分的细节|
|<**dialog**>|定义对话框，比如提示框|
|<**summary**>|标签包含 details 元素的标题|
|<**figure**>|规定独立的流内容（图像、图表、照片、代码等等）|
|<**figcaption**>|定义 <**figure**> 元素的标题|
|<**footer**>|定义 section 或 document 的页脚|
|<**header**>|定义文档的头部区域|
|<**mark**>|定义带有记号的文本|
|<**meter**>|定义度量衡,仅用于已知最大和最小值的度量|
|<**nav**>|定义运行中的进度（进程）；导航|
|<**progress**>|定义任何类型的任务的进度|
|<**ruby**>|定义 ruby 注释（中文注音或字符）|
|<**rt**>|定义字符（中文注音或字符）的解释或发音|
|<**rp**>|在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容|
|<**section**>|定义文档中的节（section、区段）|
|<**time**>|定义日期或时间|
|<**wbr**>|规定在文本中的何处适合添加换行符|

**html5已移除的元素：**

<**acronym**>
<**applet**>
<**basefont**>
<**big**>
<**center**>
<**dir**>
<**font**>
<**frame**>
<**frameset**>
<**noframes**>
<**strike**>
<**tt**>

### （2）html5新增API

（1）除了原先的DOM接口，HTML5增加了更多样化的API，下面列出一些个人觉得很不错的学习资源:

•	HTML Geolocation (地理定位) http://www.cnblogs.com/lhb25/archive/2012/07/10/html5-geolocation-api-demo.html

•	HTML Drag and Drop（拖放）
http://www.cnblogs.com/wpfpizicai/archive/2012/04/07/2436454.html

•	HTML LocalStorage（本地存储）
http://www.w3school.com.cn/html5/html_5_webstorage.asp

•	HTML Application Cache（应用缓存）
http://www.cnblogs.com/yexiaochai/p/4271834.html

•	HTML Web Workers（运行在后台的js,不会影响页面性能）
http://www.w3school.com.cn/html5/html_5_webworkers.asp

•	HTML SSE（服务器数据推送）
http://www.runoob.com/html/html5-serversentevents.html

Html SSE与websocket对比：
http://www.php100.com/html/it/biancheng/2015/0323/8828.html
	
•	HTML Canvas/WebGL（绘图）
http://blog.csdn.net/talking12391239/article/details/8646462

•	HTML Audio/Video（音频视频）
http://www.360doc.com/content/15/0317/14/14006402_455807117.shtml

#（3）html中重要的概念

**1 Canvas 与 SVG 的比较**

HTML5 支持内联 SVG（即：可伸缩矢量图形 (Scalable Vector Graphics)），使用<**svg**>标签表示。

**canvas 与 SVG 之间的一些不同之处：**

|Canvas|SVG|
|:--|:--|
|依赖分辨率|不依赖|
|不支持事件处理器|支持|
|弱的文本渲染能力|最适合带有大型渲染区域的应用程序（比如谷歌地图）|
|能够以 .png 或 .jpg 格式保存结果图像|复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）|
|最适合图像密集型的游戏，其中的许多对象会被频繁重绘|不适合游戏应用|

**2 HTML5 新的 Input 类型**

color
date
datetime
datetime-local
email
month
number
range
search
tel
time
url
week





## 三 使用实践及案例

## 

## 四 资源

### 1官网

html5中国

[http://www.html5cn.org/](http://www.html5cn.org/)

### 2文档

### 3源码

### 4教程

#### （1）已学习：



#### （2）学习中：



#### （3）待学习：

官方教程：

其他教程：

HTML5 中文教程（极客学院wiki）
http://wiki.jikexueyuan.com/project/html5/

### 5工具与资源



