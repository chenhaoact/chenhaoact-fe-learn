#TODO

比如：
（1）使用happypack(**多进程并行打包构建**)

（2）增强 uglifyPlugin：
当webpack build进度走到如80%前后时，发生很长一段时间的停滞，这一过程是uglfiyJS在对output中的bunlde部分进行压缩耗时过长导致，对此推荐使用[webpack-uglify-parallel](https://github.com/tradingview/webpack-uglify-parallel)来提升压缩速度（**多线程并行压缩**）。



待实践：
webpack 构建性能优化策略小结
https://segmentfault.com/a/1190000007891318
