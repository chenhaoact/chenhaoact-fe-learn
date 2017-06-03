# 标题

## 一 简介

### 1用途

### 2优缺点及对比

## 二 基本概念

### webpack命令及参数：

直接打包某文件为某文件：

webpack 打包文件名称（如a.js）打包后文件名称（如a.bundle.js）

使用webpack配置文件（读取webpack.config.js的配置执行webpack打包等任务）：

webpack --config webpack.config.js



加参数：

--watch  每次文件更新后自动打包自动更新

--progress  显示打包过程，会显示打包完成百分比

--display-modules 显示打包的所有模块以及通过什么loader处理都列出来

--display-reasons 为什么打包这个模块，哪里会用到显示出来

--color 打包的字是彩色的



经常将webpack命令放在npm脚本中：

在package.json中的scripts下：

"dev": "webpack --config webpack.config.js --progress --display-modules --colors --display-reason"

则执行 npm run dev 就会执行dev后面的一长串命令。



### webpack打包后的文件解析：

webpack在打包后的文件中会生成一些自己的函数，比如：\_\_webpack\_require\_\_\(模块编号数字\) 会给打包的代码模块进行编号方便引用，比如第一个函数编号为0，编号在注释里有。

处理其他文件需要loader，比如处理css文件的css-loader（让webpack支持处理css文件），style-loader（使css在html中生效，css生成style标签插入到html的head中）

### webpack1配置：

配置参考[http://webpack.github.io/docs/configuration.html](http://webpack.github.io/docs/configuration.html)

## 三 使用案例

进入项目目录\(这里我把webpack1的s实践项目放在了/project/front/webpack/webpack1-learn-project下\)，安装webpack：

npm install webpack --save

创建webpack配置文件如webpack.config.js：

配置参考[http://webpack.github.io/docs/configuration.html](http://webpack.github.io/docs/configuration.html)

用webpack --config webpack.config.js命令读取webpack.config.js的配置执行webpack打包等任务，

`module.exports = { //common.js的模块导出`

`entry:'./src/script/main.js', //打包入口从哪里开始`

`output:{`

`}`

`}`







## 四 资源

### 1官网

[http://webpack.github.io/](http://webpack.github.io/)

### 2文档

[http://webpack.github.io/docs/](http://webpack.github.io/docs/)

### 3源码

1.x最后一版：

[https://github.com/webpack/webpack/tree/v1.15.0](https://github.com/webpack/webpack/tree/v1.15.0)

### 4教程

官方教程：

[http://webpack.github.io/docs/tutorials/getting-started/](http://webpack.github.io/docs/tutorials/getting-started/)

慕课网视频教程：webpack深入与实战

[http://www.imooc.com/learn/802](http://www.imooc.com/learn/802)

