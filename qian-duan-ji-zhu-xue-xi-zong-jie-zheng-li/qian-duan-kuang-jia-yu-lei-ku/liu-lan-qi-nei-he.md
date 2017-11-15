## 简介
浏览器内核可以分成两部分：**渲染引擎 和 JS 引擎。**开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，所以**现在讲浏览器内核主要说的就是渲染引擎**。


### PC浏览器
**Chrome： Blink**
**Safari： webkit**
Mozilla FireFox： Gecko
IE（6-11）： Trident

国内
360安全浏览器 ：1.0-5.0为Trident，6.0为Trident+Webkit，7.0后为Trident+Blink；

360极速浏览器：7.5之前为Trident+Webkit,7.5后为Trident+Blink；


### 移动端浏览器
只有opera用的是一个奇怪的内核，firefox用的是另一个奇怪的内核。
其他**大部分的手机浏览器都是webkit内核**。可以这么简单粗暴的说。
UC的内核也是webkit

具体可以参考此文：
移动端浏览器有哪些，内核分别是什么
http://www.cnblogs.com/diantao/p/5292704.html



### Chrome和Chromium两个浏览器的区别
Chromium浏览器是谷歌为发展自家的浏览器Chrome而开启的计划，所以Chromium相当于Chrome的工程版或称实验版（尽管Chrome自身也有β版阶段），新功能会率先在Chromium上实现，待验证后才会应用在Chrome上。




## 参考
常见的浏览器内核
http://www.jianshu.com/p/6efcccb5ed43

移动端浏览器有哪些，内核分别是什么
http://www.cnblogs.com/diantao/p/5292704.html

浏览器内核检测工具
https://liulanmi.com/labs/core.html