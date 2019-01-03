# umd规范
UMD (Universal Module Definition), 希望提供一个前后端跨平台的解决方案(支持AMD与CommonJS模块方式),。

实现原理
UMD的实现很简单：

先判断是否支持Node.js模块格式（exports是否存在），存在则使用Node.js模块格式。
再判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块。
前两个都不存在，则将模块公开到全局（window或global）。
