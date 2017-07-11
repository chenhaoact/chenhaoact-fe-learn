#webpack代码拆分-按需加载
**可以把你的代码分离到不同的 bundle 中，然后你就可以去按需加载这些文件。**

**例如，当用户导航到匹配的路由，或用户触发了事件时，加载对应文件。**

如果使用了正确的使用方式，这可以使我们有更小的 bundle，同时**可以控制优先加载资源**，从而对你的应用程序加载时间产生重要影响。

## 分离第三方库(vendor)
一个典型的应用程序，会依赖于许多提供框架/功能需求的第三方库代码。不同于应用程序代码，这些第三方库代码不会频繁修改。

如果我们**将第三方库中的代码，保留到与应用程序代码相独立的 bundle 上，就可以利用浏览器缓存机制，把这些文件长时间的缓存到用户的机器**上。

为了完成此目标，不管应用程序代码如何变化，vendor 文件名中的 hash 部分都必须保持不变。

参考：
[使用 CommonsChunkPlugin 分离 vendor/library 代码。](http://www.css88.com/doc/webpack2/guides/code-splitting-libraries)

##分离CSS
将样式分离到单独的 bundle 中，与应用程序的逻辑分离。 这加强了样式的可缓存性，并且**浏览器能并行加载应用程序代码中的样式文件，避免无样式内容造成的闪烁问题**。

参考：
[使用 ExtractTextWebpackPlugin 来分离 css](http://www.css88.com/doc/webpack2/guides/code-splitting-css)。

##按需分离-如：使用 require.ensure() 分离代码

**资源分离，需要用户预先在配置中指定分离模块**，但**也可以在应用程序代码中创建动态分离模块**。

这可以**用于更细粒度的代码块，如，根据我们的应用程序路由，或根据用户行为预测。这可以使用户按实际需要加载非必要资源**。

###使用 require.ensure() 分离代码

**require.ensure() 是 CommonJS 异步引入资源的方法**。

**通过添加 require.ensure([<fileurl>])，在代码中定义一些需要分离的模块。这样 webpack 能够在这些分离模块内部，创建包含内部所有代码的独立 bundle**。 

参考：
[使用 require.ensure() 来分离代码。
](http://www.css88.com/doc/webpack2/guides/code-splitting-require)















