## 生产环境与开发环境构建拆分
### webpack-merge（可以把不同文件的webpack配置合并)

比如把webpack.base.js和webpack.product.js合并
https://github.com/survivejs/webpack-merge

使用参考：
webpack生产环境构建
https://doc.webpack-china.org/guides/production/

## 可视化分析：
### webpack-bundle-analyzer 分析模块大小

使用插件webpack-bundle-analyzer来可视化分析包的大小：

https://github.com/th0r/webpack-bundle-analyze

### webpack-dashboard

webpack-dashboard是用于改善开发人员使用webpack时控制台用户体验的一款工具。它摒弃了webpack（尤其是使用dev server时）在命令行内诸多杂乱的信息结构，为webpack在命令行上构建了一个一目了然的仪表盘(dashboard)，其中包括构建过程和状态、日志以及涉及的模块列表。有了它，你就可以更加优雅的使用webpack来构建你的代码。

使用注意：
使用时webpack的配置文件需要放在项目根目录下（和build同级而非封装在webpack目录下），否则因路径不匹配可能出现插件分析的构建文件找不到。

使用参考：
https://github.com/FormidableLabs/webpack-dashboard

https://yaowenjie.github.io/front-end/using-webpack-dashboard

