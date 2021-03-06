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

### 4.loader的概念以及webpack常用Loader

loader，接受资源文件作为参数，处理完会返回新的资源。各个loader可以连接起来使用，可以是同步或异步（node下运行）。可通过npm安装。

配置中的test属性可使用正则表达式进行文件类型的匹配。

注意，这里是正则表达式，不是把正则表达式写在' '字符串里，那样匹配不了任何文件，loader也就不起任何作用！

 

```
module: {
    loaders: [
      {
        test: '/\.js$/',//处理什么文件
        loader: 'babel', //使用什么什么loader,多个loader处理应使用loaders并以！串联
        exclude: './node_modules', //loader处理的排除范围哪些不需要处理
        include: '', //处理的范围，哪些必须被处理
      }
    ]
  },
```

**webpack1 loader使用参考：**

[http://webpack.github.io/docs/loaders.html](http://webpack.github.io/docs/loaders.html)

**官方列出的loader列表（各种各样的loader都可以在这里找到）：**

[http://webpack.github.io/docs/list-of-loaders.html](http://webpack.github.io/docs/list-of-loaders.html)

### 常用loader:

#### （1）babel

处理js文件，es6代码（目前大多数浏览器还不能解析）转为es5（目前大多数浏览器能解析），以支持es6编码。

[https://babeljs.io/](https://babeljs.io/)

webpack1下安装

```
npm install --save-dev babel-loader babel-core
```

#### （2）**css-loader和style-loader**

处理css文件的css-loader（让webpack支持处理css文件,js等文件中就可以引用css）。

参考：[https://github.com/webpack-contrib/css-loader](https://github.com/webpack-contrib/css-loader)

style-loader（使css在html中生效，css生成style标签插入到html的head中\)

参考：[https://github.com/webpack-contrib/style-loader](https://github.com/webpack-contrib/style-loader)

#### （3）post**css-loader**

支持postcss

[https://github.com/postcss/postcss-loader](https://github.com/postcss/postcss-loader)

#### （4）less-loader

支持less处理

[https://github.com/webpack-contrib/less-loader](https://github.com/webpack-contrib/less-loader)

#### （5）sass-loader

支持sass和scss处理

[https://github.com/webpack-contrib/sass-loader](https://github.com/webpack-contrib/sass-loader)

#### （6）处理模板文件的一些loader（如处理html文件及片段,ejs,jade,jsx的等）

http://webpack.github.io/docs/list-of-loaders.html\#templating

html-loader 处理html文件及模板片段

https://github.com/webpack-contrib/html-loader

注：jsx已经在babel-loader及其插件里支持了，设置babel即可，另外vue的插件也可以在vue中的render\(\)支持jsx。

#### （6）处理资源文件的loader

#### file-loader

https://github.com/webpack-contrib/file-loader

#### url-loader

https://github.com/webpack-contrib/url-loader

和file-loader类似，可以指定一些参数，如limit,当图片，文件等大小大于指定的limit时，就会丢给file-loader处理，小于时，转为base64编码，直接以编码打到html中去解析展示。

和file-loader对比：

通过file-loader打包的文件可以获得浏览器缓存的遍历，下一次加载时性能好。

url-loader则减少了小图片xiao文件请求的数目。

**这里个人推荐用file-loader\(因为本身应用的整体js已经比较大了，不要再把图片达成base64编码去增加其规模\)，不要因为图等文件影响应用js和css的加载渲染速度。**



#### image-loader

https://github.com/tcoopman/image-webpack-loader

配合file-loader或url-loader，可以压缩图片文件大小,默认可以压缩几倍到几十倍，压缩比与质量也可以灵活配置。

mac上需要用最新的[homebrew](https://brew.sh/)安装libpng: brew install libpng

 

#### 

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

[https://segmentfault.com/a/1190000004511992](https://segmentfault.com/a/1190000004511992)

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

代码可参考

[https://github.com/manlili/webpack\_learn](https://github.com/manlili/webpack_learn)

webpack支持多页面:

基于webpack的前端工程化开发之多页站点篇（一）

[https://segmentfault.com/a/1190000004511992](https://segmentfault.com/a/1190000004511992)

