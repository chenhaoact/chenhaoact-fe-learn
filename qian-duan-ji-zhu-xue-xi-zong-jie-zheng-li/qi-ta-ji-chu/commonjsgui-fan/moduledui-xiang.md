#CommonJS module对象

## module对象的属性

每个模块内部，都有一个module对象，代表当前模块。它有以下属性。

module.id 模块的识别符，通常是带有绝对路径的模块文件名。
module.filename 模块的文件名，带有绝对路径。
**module.loaded** 返回一个布尔值，表示模块**是否已经完成加载**。
**module.parent 返回一个对象，表示调用该模块的模块。**
**module.children 返回一个数组，表示该模块要用到的其他模块。**
module.exports 表示模块对外输出的值。