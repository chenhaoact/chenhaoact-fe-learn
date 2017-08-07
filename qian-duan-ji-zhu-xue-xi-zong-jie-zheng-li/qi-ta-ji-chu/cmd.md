# CMD

CMD (Common Module Definition), 是seajs推崇的规范，CMD是依赖就近，用的时候再require。它写起来是这样的：

define(function(require, exports, module) {
   var clock = require('clock');
   clock.start();
});

**AMD和CMD最大的区别是对依赖模块的执行时机处理不同**，而不是加载的时机或方式不同，二者皆为异步加载模块。

**AMD依赖前置，js可以方便知道依赖模块是谁，立即加载**；

**而CMD就近依赖，需要使用把模块变为字符串解析一遍才知道依赖哪些模块**，这是很多人诟病CMD的一点，牺牲性能来带来开发的便利性，实际上解析模块用的时间短到可以忽略。

参考：
AMD 和 CMD 的区别有哪些？
https://www.zhihu.com/question/20351507

JS 的模块化编程（四）- CMD
http://anjia.github.io/2015/06/23/js_module_2_CMD/

