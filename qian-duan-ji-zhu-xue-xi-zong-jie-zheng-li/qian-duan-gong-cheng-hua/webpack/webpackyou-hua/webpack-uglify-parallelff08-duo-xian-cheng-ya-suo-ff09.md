 # webpack-uglify-parallel
多线程压缩，对于大的项目，要压缩的文件比较多（有时构建时出现在80%的时候要等好长时间就是这个问题），使用此插件，可以有效的提升构建的效率（比如从180s减少到50多秒）

https://github.com/tradingview/webpack-uglify-parallel

## 注意（采坑总结）：
1. 此插件和preact有变量上的冲突，**所以preact的项目建议不要使用此插件**，**可能造成构建后页面不报错却白屏**的问题。
 
 