### devtool
可以在浏览器的资源文件夹下生产webpack目录，映射到项目的各个文件，方便打断点调试和定位问题根源，建议dev环境配置为 "#eval-source-map"，production环境下配置为"#source-map"。

https://doc.webpack-china.org/configuration/devtool/

#### 什么是source-map？
**Source map**就是一个信息文件，里面储存着位置信息。即：**转换后代码的每个位置，所对应的转换前的位置**。

有了它，出错时，除错**工具将直接显示原始代码，而不是转换后的代码**。这无疑给开发者带来了很大方便。

参考：
JavaScript Source Map 详解
http://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html

[webpack] devtool里的7种SourceMap模式是什么鬼？
https://juejin.im/post/58293502a0bb9f005767ba2f