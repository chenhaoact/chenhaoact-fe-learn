# Webpack2学习总结

（注：以下内容是我学习webpack2[官方英文教程](https://webpack.js.org/guides/)和[官方英文文档](https://webpack.js.org/configuration/)的收货整理，个人坚持学习任何技术以官方文档为准的原则）

## 一 简介

### 1用途

构建应用程序中的 JavaScript 模块。

快速建立应用程序依赖图表并以正确的顺序打包它们以简化工作流。

### 2优缺点及对比

在 webpack 1 中，可以使用[`require.ensure`](https://doc.webpack-china.org/guides/code-splitting-async/#require-ensure-)作为实现应用程序的懒加载 chunks 的一种方法，webpack2中使用ES2015 的代码分割，ES2015 模块加载规范定义了[`import()`](https://doc.webpack-china.org/guides/code-splitting-async)方法，可以在运行时\(runtime\)动态地加载 ES2015 模块。

webpack 现在支持在配置文件中返回`Promise`了，因此可以在配置文件中做异步处理。

webpack v1只支持能够「可`JSON.stringify`的对象」作为 loader 的 options。webpack v2 现在支持任何js对象作为 loader options.

## 二 基本概念



### 2 webpack2常用插件



（4）clean-webpack-plugin 

构建之前先删除如dist或build等目录下面的文件夹及文件

https://github.com/johnagan/clean-webpack-plugin



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

把new webpack.optimize.CommonsChunkPlugin\('vendors', 'vendors.js'\),改写为

```
new webpack.optimize.CommonsChunkPlugin\({ name: 'vendor', filename: 'vendors.js' }\),
```

#### （3）按照webpack2的规则修改webpack配置文件

#### 详细可以参考：

[https://doc.webpack-china.org/guides/migrating/](https://doc.webpack-china.org/guides/migrating/)

**详细配置写法参考**

[https://doc.webpack-china.org/configuration/](https://doc.webpack-china.org/configuration/)

或者按照命令中的错误提示一步一步修改也可以，**建议按照上面的**[**官方的升级文档**](https://doc.webpack-china.org/guides/migrating/)**和**[**详细配置**](https://doc.webpack-china.org/configuration/)**系统的去修改，效率更高一些**，而且能系统的了解webpack1和2的写法区别，以下是我的详细修改步骤：

首先：

module.loaders 改为 module.rules;

如果有链式调用的loader ，上一个 loader 的输出被作为输入传给下一个 loader。使用[rule.use](https://doc.webpack-china.org/configuration/module#rule-use)配置选项，`use`可以设置为一个 loader 数组。 在 webpack 1 中，loader 通常被用`!`连写。这一写法在 webpack 2 中只在使用旧的`module.loaders`时才有效。建议使用rule.use而非! ;

在引用 loader 时，不能再省略`-loader`后缀了;

移除 module.preLoaders 和 module.postLoaders，统一放在module.rules下；

`webpack.optimize.DedupePlugin`抽取出输出包体中的相同或者近似的文件或者代码，能有效地减少包体大小，提升性能。webpack2中不再需要webpack.optimize.DedupePlugin  ，从配置中移除;

[ExtractTextPlugin](https://github.com/webpack/extract-text-webpack-plugin) 需要使用版本 2，才能在 webpack 2 下正常运行，

`npm install --save-dev extract-text-webpack-plugin`

这一插件的配置变化主要体现在语法上；

不能再通过`webpack.config.js`的自定义属性来配置 loader。只能通过`options`来配置loader，典型的`options`

被称为`query`，是一个可以被添加到 loader 名之后的字符串。它比较像一个 query string，但是实际上有[更强大的能力](https://github.com/webpack/loader-utils#parsequery)；

这些都按官方文档做完后，在执行npm run dev，根据终端 中错误提示来修改：

![](/assets/importcw1.png)

把

`new webpack.optimize.CommonsChunkPlugin('vendors', 'vendors.js'),`

改写为

`new webpack.optimize.CommonsChunkPlugin({ name: 'vendor', filename: 'vendors.js' }),`

然后需要把所有的插件重新卸载安装并按照github或npm上的说明重写按照webpack2的配置写。

## 四 资源与参考

### 1官网

[https://webpack.js.org](https://webpack.js.org)

webpack官网中文版

[https://doc.webpack-china.org/](https://doc.webpack-china.org/)

### 2文档

[https://webpack.js.org/configuration/](https://webpack.js.org/configuration/)

**中文文档（包括配置详细规则\)**

[**https://doc.webpack-china.org/configuration/**](https://doc.webpack-china.org/configuration/)

**官方推荐的所有loaders详细介绍**

[https://doc.webpack-china.org/loaders/](https://doc.webpack-china.org/loaders/)

**官方推荐的所有plugins详细介绍**

[https://doc.webpack-china.org/plugins/](https://doc.webpack-china.org/plugins/)

### 3源码

[https://github.com/webpack/webpack](https://github.com/webpack/webpack)

### 4教程

官方教程（建议先看这个）：

[https://webpack.js.org/guides/](https://webpack.js.org/guides/)

官方教程中文版：

[https://doc.webpack-china.org/guides/](https://doc.webpack-china.org/guides/)

webpack 2 的新特性:

[https://qiutc.me/post/webpack-2-的新特性-What-s-new-in-webpack-2.html](https://qiutc.me/post/webpack-2-的新特性-What-s-new-in-webpack-2.html)

webpack 2 入门

[http://www.css88.com/archives/6992](http://www.css88.com/archives/6992)

webpack2 终极优化:

[http://imweb.io/topic/5868e1abb3ce6d8e3f9f99bb](http://imweb.io/topic/5868e1abb3ce6d8e3f9f99bb)

