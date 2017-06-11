# webpack学习实践整理

## 一 简介

### 1用途

### 2优缺点及对比

## 二 基本概念及技术重点

### 1.webpack命令及参数：

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

### 2.webpack打包后的文件解析：

webpack在打包后的文件中会生成一些自己的函数，比如：\_\_webpack\_require\_\_\(模块编号数字\) 会给打包的代码模块进行编号方便引用，比如第一个函数编号为0，编号在注释里有。

处理其他文件需要loader，比如**处理css文件的css-loader（让webpack支持处理css文件），style-loader（使css在html中生效，css生成style标签插入到html的head中**）

### 3.webpack1配置：

配置参考[http://webpack.github.io/docs/configuration.html](http://webpack.github.io/docs/configuration.html)

#### \(1\)entry（入口）和output（生成文件）

entry可以是字符串，数组，或对象，打包多个入口文件要设置为对象，同事output的filename，chunkFilename等不能写死，要用\[name\] ，\[hash\] （**hash值就相当于是文件的版本号，是经过md5加密处理的，每次文件修改后的hash值都会变（对项目上线迭代很有用）**）这些生成的变量代替（[具体看配置文档中的output部分](http://webpack.github.io/docs/configuration.html#output)）：

```
{
    entry: {
        page1: "./page1",
        page2: ["./entry1", "./entry2"]
    },
    output: {
        // Make sure to use [name] or [id] in output.filename
        //  when using multiple entry points
        filename: "[name].bundle.js",
        chunkFilename: "[id].bundle.js"
    }
}
```

### 

### 4.webpack常用Loader

#### （1）**css-loader和style-loader**

处理css文件的css-loader（让webpack支持处理css文件），style-loader（使css在html中生效，css生成style标签插入到html的head中

### 

### 5.webpack常用插件

webpack1插件使用参考：[http://webpack.github.io/docs/plugins.html](http://webpack.github.io/docs/plugins.html)

#### （1）html-webpack-plugin

对html文件进行打包并把需要的webpack中定义的js标签插入到html中（而且支持页面中直接写ejs模板引擎代码进行一些控制），并满足很多种处理和生产html文件的需求，具体参考：  
[https://github.com/jantimon/html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)

## 三 使用案例

### 1.项目安装webpack\(这里是webpack1.15.0\):

进入项目目录\(这里我把webpack1的s实践项目放在了/project/front/webpack/webpack1-learn-project下\)，安装webpack：

npm install webpack --save-dev

创建webpack配置文件如webpack.config.js：

配置参考[http://webpack.github.io/docs/configuration.html](http://webpack.github.io/docs/configuration.html)

用webpack --config webpack.config.js命令读取webpack.config.js的配置执行webpack打包等任务，

```
module.exports = { //common.js的模块导出

entry:'./src/script/main.js', //打包入口从哪里开始

output:{
path: './build',
filename: "js/[name]-[chunkhash].js" //打包的文件使用name+chunkhash命名一遍更新迭代和保密,js会放在js文件夹下
}

}
```

npm 中添加命令脚本如下：

```
"scripts": {
    "dev": "webpack-dev-server --progress --profile --colors --hot --inline",
    "build": "webpack --progress --profile --colors"
  },
```

之后只需要执行：

```
npm run dev    开发
npm run build   生产环境下打包构建
```

执行npm run build，会发现打包的代码已经到build目录下了。

### 2.支持多页面

然后添加webpack.config.js配置如下，（这里用到了html-webpack-plugin插件（需npm安装））以支持多页面：

```
const HtmlwebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: { //多个页面入口
        main: "./src/index.js", //主页面
        page2: "./src/pages/page2/index.js",
        page3: "./src/pages/page3/index.js"
    },
    output: {
        path: './build',
        filename: "js/[name]-[chunkhash].js" //打包的文件使用name+chunkhash命名一遍更新迭代和保密,js会放在js文件夹下
    },
    plugins: [
        //对各html文件进行处理和打包,多个页面就多次调用插件函数HtmlwebpackPlugin对每个html文件进行处理即可
        //主页面
        new HtmlwebpackPlugin({
            template: 'index.html', //对根目录下的那个html文件打包并插入上面的js
            filename: 'index.html', //多个页面必须要有不同的template和生成的filename，否则只生成一个文件
            chunks: ['main'] //页面用到了哪些入口文件，每个页面最好只引用自己需要的js(对应上面的entry写)
        }),
        //page2
        new HtmlwebpackPlugin({
            template: 'page2.html',
            filename: 'page2.html',
            chunks: ['page2']
        }),
        //page3
        new HtmlwebpackPlugin({
            template: 'page3.html',
            filename: 'page3.html',
            chunks: ['page3']
        })
    ]
}
```

gen目录下添加几个html，指定调用的js为pages下的page2,和page3下的index.js,执行npm run build会发现，打包好的各个页面的html和js。如下图：

![](/assets/QQ20170606-213750@2x.png)

更多webpack支持多页面的介绍可参考：

基于webpack的前端工程化开发之多页站点篇（一）

https://segmentfault.com/a/1190000004511992



### 3.

### 

## 四 资源与参考

### 1官网

[http://webpack.github.io/](http://webpack.github.io/)

### 2文档

[http://webpack.github.io/docs/](http://webpack.github.io/docs/)

webpack1所有配置说明：

[http://webpack.github.io/docs/configuration.html](http://webpack.github.io/docs/configuration.html)

### 3源码

1.x最后一版：

[https://github.com/webpack/webpack/tree/v1.15.0](https://github.com/webpack/webpack/tree/v1.15.0)

### 4教程

官方教程：

[http://webpack.github.io/docs/tutorials/getting-started/](http://webpack.github.io/docs/tutorials/getting-started/)

慕课网视频教程：webpack深入与实战

[http://www.imooc.com/learn/802](http://www.imooc.com/learn/802)

webpack支持多页面:

基于webpack的前端工程化开发之多页站点篇（一）

https://segmentfault.com/a/1190000004511992



