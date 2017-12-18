# 浏览器兼容性查询

Mdn下面会有相应方法基本的兼容性，查具体的兼容性可以用[caniuse](http://caniuse.com/) ,**也支持查询js兼容性的**.

比如要查 Object.assign，就输入Object查询，下面寻找.assign方法，点击去查询。

如果需要兼容的浏览器不支持，就需要引入[babel-polifill](https://babeljs.io/docs/usage/polyfill/)或者把MDN下面的polifill里的实现方法拷贝到项目中作为实现工具方法，再调用，否则会因为兼容性问题在特性浏览器下报错。

建议PC和对性能要求不高的项目直接引入

