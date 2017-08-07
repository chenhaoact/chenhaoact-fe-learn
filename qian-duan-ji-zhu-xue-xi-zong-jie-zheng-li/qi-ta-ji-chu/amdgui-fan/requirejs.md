# require.js的用法

**require.js加载的模块，采用AMD规范。**

模块采用define()函数定义。

如果一个模块不依赖其他模块，可直接定义在define()函数中：

现有math.js定义了一个math模块。math.js要这样写：
　　
```
// math.js
　　define(function (){
　　　　var add = function (x,y){
　　　　　　return x+y;
　　　　};
　　　　return {
　　　　　　add: add
　　　　};
　　});
```

**加载方法如下（ 用require() ）**：


```
　　// main.js
　　require(['math'], function (math){
　　　　alert(math.add(1,1));
　　});

```


**如果模块还依赖其他模块，那define()函数的第一个参数，必须是一个数组，指明该模块的依赖。**

```
　　define(['myLib'], function(myLib){
　　　　function foo(){
　　　　　　myLib.doSomething();
　　　　}
　　　　return {
　　　　　　foo : foo
　　　　};
　　});
```


**当require()函数加载上面这个模块的时候，就会先加载依赖的模块**（myLib.js文件）。

参考：

[Javascript模块化编程（三）：require.js的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
