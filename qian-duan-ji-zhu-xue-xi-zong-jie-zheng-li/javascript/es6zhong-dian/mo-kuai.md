# 模块Module

## 一 简介
ES6之前，Js 一直没有模块（module）体系，对开发大型、复杂项目形成了巨大障碍。

社区制定了一些模块加载方案，主要有 CommonJS 和 AMD。前者用于服务器，后者用于浏览器。




ES6的import，不能“动态”拼一个路径，因为ES6的模块化就是**强制静态化**，有兴趣可以Google一下为什么要静态化，以及好处。

如果要动态引入模块，建议用node(commonjs)的require。require动态引入模块路径 require()里直接放url变量会报错: Cannot find module "."， 可先加带.的路径前缀的字符串再+文件路径变量即可，如：

```
const MdUrl = 'data/' + this.props.params.id + '.md';
const MdHtml = require('../../' + MdUrl);
```

import和require的对比参考：
Node中没搞明白require和import，你会被坑的很惨
http://www.tuicool.com/articles/uuUVBv2


