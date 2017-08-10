## 三 react构建过程分析

从package.json来看npm run build命令的配置，是用node执行了scripts/rollup/build.js

![](/assets/WX20170810-115251@2x.png)

打开scripts/rollup/build.js：

![](/assets/WX20170810-135507@2x.png)

这里主要用到了[rollup](https://github.com/rollup/rollup) (Next-generation ES6 module bundler http://rollupjs.org)进行es6模块的打包处理。






















