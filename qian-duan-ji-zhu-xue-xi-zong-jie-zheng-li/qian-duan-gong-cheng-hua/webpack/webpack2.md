# Webpack2学习总结

（注：以下内容是我学习webpack2[官方英文教程](https://webpack.js.org/guides/)和[官方英文文档](https://webpack.js.org/configuration/)的收货整理，个人坚持学习任何技术以官方文档为准的原则）

## 一 简介

### 1用途

构建应用程序中的 JavaScript 模块。

快速建立应用程序依赖图表并以正确的顺序打包它们以简化工作流。

### 2优缺点及对比

## 二 基本概念

## 三 使用案例

### 1 webpack1升级到webpack2实践

#### （1）升级前

以下是我原本使用webpack1搭建项目的webpack配置webpack.config.js：

`const path = require('path');`

`const webpack = require('webpack');`

`const HtmlwebpackPlugin = require('html-webpack-plugin');`

`const ExtractTextPlugin = require("extract-text-webpack-plugin");`

`const CompressionPlugin = require("compression-webpack-plugin");`

`const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;`

`/**`

`* 文件路径定义`

`* */`

`const ROOT_PATH = path.resolve(__dirname);`

`const APP_PATH = path.resolve(ROOT_PATH, 'app');`

`const BUILD_PATH = path.resolve(ROOT_PATH, 'app/build');`

`const PAGE_PATH = path.resolve(ROOT_PATH, 'app/pages');`

`module.exports = {`

`//entry,入口，指定要打包成的文件，目前是有app.js和vendors.js`

`entry: {`

`app: path.resolve(APP_PATH, 'index.jsx'),`

`//提取第三方库，单独打包到venders.js,提升性能`

`vendors: ['react', 'react-dom', 'react-router', 'react-redux', 'moment'] //需要用到的一些库，最好单独提出来到venders比较好，不要和自己的业务代码混在一起`

`},`

`output: {`

`path: BUILD_PATH,`

`filename: '[name].js'`

`},`

`resolve: {`

`extensions: ['', '.js', '.jsx']`

`},`

`//启动dev source map，出错以后就会采用source-map的形式直接显示你出错代码的位置。`

`//完美的 SourceMaps 是很慢的，webpack 官方提供了七种 sourceMap 模式共大家选择`

`//具体参考：https://segmentfault.com/a/1190000005770042 SourceMaps一节，但暂时用cheap-source-map编译时看不到打包大小有好多黄色的提示`

`devtool: 'eval-source-map',`

`//enable dev server`

`devServer: {`

`historyApiFallback: true,`

`hot: true,`

`inline: true,`

`progress: true,`

`//只要配置dev server map这个参数就可以了`

`proxy: {`

`'/api/*': {`

`target: 'http://localhost:8080',`

`secure: false`

`}`

`}`

`},`

`//babel重要的loader在这里`

`module: {`

`//loader前执行处理，这样每次npm run start的时候就可以看到一些提示信息`

`preLoaders: [],`

`loaders: [`

`{`

`test: /\.(js|jsx)$/, //js和jsx文件都这样用babel处理`

`loader: 'babel',`

`include: APP_PATH,`

`query: {`

`//添加两个presents 使用这两种presets处理js或者jsx文件`

`presets: ['es2015', 'react'],`

`// ant-d官网推荐以这种方式引入ant-d组件的样式可以使得样式也按需加载，减少打包文件的大小提高性能,需要先安装babel-plugin-import，`

`// 参考：https://github.com/ant-design/babel-plugin-import`

`plugins: [`

`['import', [{libraryName: "antd", style: 'css'}]],`

`],`

``// This is a feature of `babel-loader` for webpack (not Babel itself).``

`// It enables caching results in ./node_modules/.cache/babel-loader/`

`// directory for faster rebuilds.`

`cacheDirectory: true`

`}`

`},`

`//eslint校验，TODO:暂时先去掉，把webstorm的eslint提示和自动format弄好再开`

`// {`

`//   test: /\.js$/,`

`//   exclude: /node_modules/,`

`//   loader: 'eslint-loader'`

`// },`

`//原来 css-loader的配置，现在加用下面的插件extract-text-webpack-plugin`

`// {`

`//   test: /\.css$/,`

`//   loader: 'style-loader!css-loader'`

`// },`

`// {`

`//   test: /\.scss$/,`

`//   loaders: ['style', 'css', 'sass']`

`// }`

`//使用插件，将css单独打包，不打入js,提升页面加载速度和性能，参考插件使用：https://github.com/webpack-contrib/extract-text-webpack-plugin`

`{`

`test: /\.css$/,`

`loader: ExtractTextPlugin.extract("style-loader", "css-loader")`

`},`

`{`

`test: /\.scss$/,`

`loader: ExtractTextPlugin.extract("style-loader", "css-loader!sass-loader")`

`}`

`]`

`},`

`plugins: [`

`//设置合适的环境变量能够，需要在生产环境中将NODE_ENV设置为production，`

`// 帮助 Webpack 更好地去压缩处理依赖中的代码,减少包体大小,提升性能`

`new webpack.DefinePlugin({ // <-- key to reducing React's size`

`'process.env': {`

`'NODE_ENV': JSON.stringify('production')`

`}`

`}),`

`//抽取出输出包体中的相同或者近似的文件或者代码，可能对于 Entry Chunk 有所负担，不过能有效地减少包体大小，提升性能。`

`new webpack.optimize.DedupePlugin(),`

`//使用插件，将css单独打包，不打入js,提升页面加载速度和性能，参考插件使用：https://github.com/webpack-contrib/extract-text-webpack-plugin`

`new ExtractTextPlugin('style.css'),`

`//使用uglifyJs压缩js代码，提升性能。`

`new webpack.optimize.UglifyJsPlugin({`

`minimize: true //此配置已经是最小了，默认已去掉了注释等，不需要其他的配置`

`}),`

`//ignoreplugin :用于忽略引入模块中并不需要的内容，减少打包文件大小，提升性能。譬如当我们引入moment.js时，我们并不需要引入该库中所有的区域设置，因此可以利用该插件忽略不必要的代码。`

`new webpack.IgnorePlugin(/^\.\/locale$/, [/moment$/]),`

`//默认的页面在PAGE_PATH下的index.html`

`new HtmlwebpackPlugin({`

`title: 'My first react app',`

`template: path.resolve(PAGE_PATH, 'index.html'),`

`filename: 'index.html',`

`chunks: ['app', 'vendors'],`

`inject: 'body'`

`}),`

`// 把入口文件里面的数组打包,合并区块成verdors.js，`

`// 这个插件的功能是将多个打包结果中公共的部分抽取出来，作为一个单独的文件。它符合目前的场景，因为 main.js 和 vendor.js 中存在一份公共的代码，那就是 vendor.js 中的内容`

`new webpack.optimize.CommonsChunkPlugin('vendors', 'vendors.js'),`

`//使用compression-webpack-plugin插件,将资源文件压缩为.gz文件，并且根据客户端的需求按需加载，提升性能。`

`new CompressionPlugin({`

`asset: "[path].gz[query]",`

`algorithm: "gzip",`

`test: /\.js$|\.css$|\.html$/,`

`threshold: 10240,`

`minRatio: 0`

`}),`

`//使用插件webpack-bundle-analyzer来可视化分析包的大小：https://github.com/th0r/webpack-bundle-analyze 以便提升性能。`

`new BundleAnalyzerPlugin()`

`]`

`}`

我升级前使用webpack1时的package.json：

`{`

`"name": "my-website",`

`"version": "1.0.0",`

`"description": "陈浩的个人网站",`

`"main": "index.jsx",`

`"scripts": {`

`"dev": "webpack-dev-server --progress --profile --colors --hot --inline",`

`"build": "webpack --progress --profile --colors",`

`"test": "test"`

`},`

`"author": "chenhaoact",`

`"license": "ISC",`

`"devDependencies": {`

`"babel-core": "^6.22.1",`

`"babel-loader": "^6.2.10",`

`"babel-plugin-import": "^1.1.1",`

`"babel-plugin-lodash": "^3.2.11",`

`"babel-polyfill": "^6.22.0",`

`"babel-preset-es2015": "^6.22.0",`

`"babel-preset-es2015-node6": "^0.4.0",`

`"babel-preset-react": "^6.22.0",`

`"babel-preset-stage-3": "^6.22.0",`

`"compression-webpack-plugin": "^0.4.0",`

`"css-loader": "^0.26.1",`

`"eslint": "^3.14.1",`

`"eslint-config-airbnb": "^14.0.0",`

`"eslint-loader": "^1.6.1",`

`"eslint-plugin-import": "^2.2.0",`

`"eslint-plugin-jsx-a11y": "^3.0.2",`

`"eslint-plugin-react": "^6.9.0",`

`"extract-text-webpack-plugin": "^1.0.1",`

`"file-loader": "^0.9.0",`

`"html-webpack-plugin": "^2.26.0",`

`"jshint": "^2.9.4",`

`"jshint-loader": "^0.8.3",`

`"mocha": "^3.2.0",`

`"moment": "^2.17.1",`

`"node-sass": "^4.3.0",`

`"redux-devtools": "^3.3.2",`

`"sass-loader": "^4.1.1",`

`"style-loader": "^0.13.1",`

`"url-loader": "^0.5.7",`

`"webpack": "^1.14.0",`

`"webpack-bundle-analyzer": "^2.4.0",`

`"webpack-dev-server": "^1.16.2"`

`},`

`"dependencies": {`

`"antd": "^2.9.3",`

`"ejs": "^2.5.6",`

`"koa": "^2.2.0",`

`"koa-bodyparser": "^2.3.0",`

`"koa-convert": "^1.2.0",`

`"koa-router": "^7.1.0",`

`"koa-static": "^2.1.0",`

`"koa-views": "^5.2.1",`

`"lodash": "^4.17.4",`

`"material-ui": "^0.16.7",`

`"mongoose": "^4.8.1",`

`"pm2": "^2.3.0",`

`"prop-types": "^15.5.8",`

`"react": "^15.5.4",`

`"react-dom": "^15.5.4",`

`"react-redux": "^5.0.4",`

`"react-router": "^3.0.5",`

`"react-tap-event-plugin": "^2.0.1",`

`"react-toolbox": "^2.0.0-beta.5",`

`"redux": "^3.6.0"`

`}`

`}`

我升级前使用webpack1时的代码目录结构：

![](/assets/importsgqq.png)

#### （2）安装最新版webpack（这里是webpack2）

因为我之前安装了webpack1，我试了下需要先卸载

```
npm uninstall --save-dev webpack
```

再安装才会到最新的版本

```
npm install --save-dev webpack
```

然后执行原来的命令：

```
npm run dev
```

发现立即报错，说明webpack2和webpack1的配置和插件写法有很大不同，下面修改配置文件。

![](/assets/import.png)

#### （3）按照webpack2的规则修改webpack配置文件

#### 详细可以参考：

[https://doc.webpack-china.org/guides/migrating/](https://doc.webpack-china.org/guides/migrating/)

**详细配置写法参考**

**https://doc.webpack-china.org/configuration/**

或者按照命令中的错误提示一步一步修改也可以，建议按照上面官方的升级文档系统的去修改，效率更高一些，而且能系统的了解webpack1和2的写法区别，以下是我的详细修改步骤：

首先：

module.loaders 改为 module.rules





## 四 资源

### 1官网

[https://webpack.js.org](https://webpack.js.org)

webpack官网中文版

[https://doc.webpack-china.org/](https://doc.webpack-china.org/)

### 2文档

[https://webpack.js.org/configuration/](https://webpack.js.org/configuration/)

**中文文档（包括配置详细规则\)**

[**https://doc.webpack-china.org/configuration/**](https://doc.webpack-china.org/configuration/)

### 3源码

[https://github.com/webpack/webpack](https://github.com/webpack/webpack)

### 4教程

官方教程（建议先看这个）：

[https://webpack.js.org/guides/](https://webpack.js.org/guides/)

官方教程中文版：

[https://doc.webpack-china.org/guides/](https://doc.webpack-china.org/guides/)

Webpack 2 入门教程:

[https://llp0574.github.io/2016/11/29/getting-started-with-webpack2/](https://llp0574.github.io/2016/11/29/getting-started-with-webpack2/)

Webpack2.x踩坑与总结

[http://mrzhang123.github.io/2017/02/07/webpack2/?utm\_source=tuicool&utm\_medium=referral](http://mrzhang123.github.io/2017/02/07/webpack2/?utm_source=tuicool&utm_medium=referral)

webpack 2 的新特性:

[https://qiutc.me/post/webpack-2-的新特性-What-s-new-in-webpack-2.html](https://qiutc.me/post/webpack-2-的新特性-What-s-new-in-webpack-2.html)

\[译\] 迁移到 webpack2，你需要知道这些:

[https://juejin.im/entry/581d9fcc8ac247004ff3c70e](https://juejin.im/entry/581d9fcc8ac247004ff3c70e)

webpack 2 入门

[http://www.css88.com/archives/6992](http://www.css88.com/archives/6992)

webpack2 终极优化:

[http://imweb.io/topic/5868e1abb3ce6d8e3f9f99bb](http://imweb.io/topic/5868e1abb3ce6d8e3f9f99bb)

