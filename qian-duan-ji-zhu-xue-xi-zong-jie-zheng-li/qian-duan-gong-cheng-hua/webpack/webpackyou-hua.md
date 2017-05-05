**搜索引擎搜索 webpack优化 就会有很多不错的文章，任何技术都应该多搜一搜看一看 ...优化 方面的文章。**

如果引用了ant-d:

ant-d按需加载\(使用babel-plugin-import 是一个用于按需加载组件代码和样式的 babel 插件：

[https://ant.design/docs/react/use-with-create-react-app-cn](https://ant.design/docs/react/use-with-create-react-app-cn) 参考高级配置和按需加载部分

实践后，app.js从 14.8MB 降到 4.79MB! 看来正确的按需加载和引用ant-d等组件库对性能很重要。

基于 Webpack 的应用包体尺寸优化

[https://zhuanlan.zhihu.com/p/24928279](https://zhuanlan.zhihu.com/p/24928279)

简单几步助你优化React应用包体

[https://segmentfault.com/a/1190000007692543](https://segmentfault.com/a/1190000007692543)

webpack + react 优化：缩小js包体积

[http://blog.csdn.net/code\_for\_free/article/details/51583737](http://blog.csdn.net/code_for_free/article/details/51583737)

彻底解决 webpack 打包文件体积过大

[http://www.jianshu.com/p/a64735eb0e2b](http://www.jianshu.com/p/a64735eb0e2b)

开发工具心得：如何 10 倍提高你的 Webpack 构建效率

[https://segmentfault.com/a/1190000005770042](https://segmentfault.com/a/1190000005770042)

webpack使用优化

[http://www.tuicool.com/articles/bAzMju](http://www.tuicool.com/articles/bAzMju)

[http://www.alloyteam.com/2016/01/webpack-use-optimization/](http://www.alloyteam.com/2016/01/webpack-use-optimization/)

webpack2 终极优化

[http://www.open-open.com/lib/view/open1483317889255.html](http://www.open-open.com/lib/view/open1483317889255.html)

## webpack及reacct优化常用方法整理

1.**各个模块，组件库，类库，按需引入，按需加载。**引入某个功能的时候，应该只引入需要的模块，以 Lodash 为例：

```
//1.Import the entire lodash library and add it to the bundle

import lodash from 'lodash'

lodash.groupBy(rows, 
'id'
)

//2.Import only the required function from lodash

import groupBy from 'lodash/groupBy'

groupBy(rows, 
'id'
)
```



再如：ant-d按需加载\(使用babel-plugin-import 是一个用于按需加载组件代码和样式的 babel 插件：https://ant.design/docs/react/use-with-create-react-app-cn 参考高级配置和按需加载部分

实践后，app.js从 14.8MB 降到 4.79MB,vendors.js为1.25MB! 看来正确的按需加载和引用ant-d等组件库对性能很重要。

（2）使用一些webpack插件减小打包文件大小，提升性能基于 Webpack 的应用包体尺寸优化https://zhuanlan.zhihu.com/p/24928279和简单几步助你优化React应用包体https://segmentfault.com/a/1190000007692543

实践后，文件进一步减小，

其中：

在生产环境中将NODE\_ENV设置为productionapp.js从4.79MB降到4.63MB,vendors.js为1.25MB

使用new webpack.optimize.DedupePlugin\(\)后app.js从降到4.51MB,vendors.js为1.25MB

使用new webpack.IgnorePlugin\(/^\.\/locale$/, \[/moment$/\]\), 用于忽略引入模块中并不需要的内容，减少打包文件大小，提升性能。譬如当我们引入moment.js时，我们并不需要引入该库中所有的区域设置，因此可以利用该插件忽略不必要的代码。app.js为4.51MB,而vendors.js则由1.25MB大幅度降到329kB（看来原来的vendors.js中moment不需要的部分就占了一大部分）

使用compression-webpack-plugin插件后,将资源文件压缩为.gz文件，并且根据客户端的需求按需加载build目录多出来了app.js.gz（1.09 MB）和vendors.js.gz（80.1 kB），可以看出，使用gz压缩后的文件比原文件小了很多由于我的服务端使用的是koa的koa-static（https://github.com/koajs/static）来加载静态资源，gzip Try to serve the gzipped version of a file automatically when gzip is supported by a client and if the requested file with .gz extension exists. defaults to true.所以如果有gzip的压缩文件会默认去解析，从而提升应用的性能。

经过这些步骤，在服务端node应用的加载所有前端资源的时间有一开始的近1min,变为了1.64s,很大的提升了性能和体验：

优化前：![](/assets/importwbpyhq.png)

优化后：

![](/assets/importwebpyh.png)

