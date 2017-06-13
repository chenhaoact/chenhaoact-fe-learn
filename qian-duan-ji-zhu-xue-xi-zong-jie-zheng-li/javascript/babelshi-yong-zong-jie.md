

latest已经被弃用，想使用最新版的es6的支持要使用env（比如像支持2017年想支持es2017）:

https://babeljs.io/docs/plugins/preset-env/

```
npm install babel-preset-env --save-dev
```



创建.babelrc

配置如下声明babel行为

```
{
"presets":["env"]
}
```



Babel 是一个 JavaScript 编译器。可以让今天就用下一代 JavaScript 语法写代码。（可以支持各种环境，如webpack,browserify，gulp等）

[https://babeljs.io/](https://babeljs.io/)

[http://babeljs.cn/](http://babeljs.cn/)

在各种环境下使用babel:

[http://babeljs.cn/docs/setup/](http://babeljs.cn/docs/setup/)

可以好好研究下babel源代码，看下是如何实现es6转es5的，对理解es6和es5很有好处：

[https://github.com/babel/babel](https://github.com/babel/babel)

babel官网的es2015教程（推荐）

[https://babeljs.io/learn-es2015/](https://babeljs.io/learn-es2015/)

babel相关插件

[https://babeljs.io/docs/plugins/](https://babeljs.io/docs/plugins/)

