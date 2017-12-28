# Module 的加载实现
## 一 在浏览器中加载 ES6 模块

### 1. 浏览器加载js的传统方法
HTML中，浏览器通过`<script>`标签加载 JS 脚本。

**浏览器默认同步加载 JS 脚本，即渲染引擎遇到`<script>`标签就会停下来，等到执行完脚本，再继续向下渲染**。如果是**外部脚本，还须加入脚本下载时间**。

如**脚本体积很大**，下载和执行时间就会很长，**易造成浏览器堵塞，“卡死”，没有任何响应**。这显然是很不好的体验，**所以浏览器允许脚本异步加载**，下面就是**两种异步加载的语法**：

** 即 `<script>`标签打开defer或async属性**，脚本就会异步加载。**渲染引擎遇到此标签时，就开始下载外部脚本，但不会等它下载和执行完，而是直接执行后面的代码**。

#### defer与async的区别：
defer要等整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），才会执行；
async一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。

一句话，**defer是“渲染完再执行”，async是“下载完就执行”**。

另外，**如有多个defer脚本，会按在页面出现的顺序加载，而多个async脚本则不能保证加载顺序（因为谁先下载完谁就执行）**。

### 2. 加载ES6模块代码的规则

**浏览器加载 ES6 模块，也使用`<script>`标签，但要加入type="module"属性**。



```
<script type="module" src="./foo.js"></script>
```



上面代码在网页中插入模块foo.js，**由于type属性设为module，所以浏览器知道这是一个 ES6 模块**。

**浏览器对于带有type="module"的<script>，都是异步加载，不会造成堵塞浏览器，即等整个页面渲染完，再执行模块脚本，等同于打开了<script>标签的defer属性**。

如果网页有多个`<script type="module">`，它们会按照在页面出现的顺序依次执行。

`<script>`标签的async属性也可以打开，这时只要加载完成，渲染引擎就会中断渲染立即执行。执行完成后，再恢复渲染。`<script type="module">`也就不会按照在页面出现的顺序执行，而是只要该模块下载完成，就执行该模块。

ES6 模块代码也允许内嵌在网页中，语法行为与加载外部脚本完全一致：


```
<script type="module">
  import utils from "./utils.js";

  // other code
</script>
```

#### 对于外部的模块脚本（上例是通过type="module" 引用foo.js文件），有几点需注意：

代码在模块作用域之中运行，而非在全局作用域运行。模块内部的顶层变量，外部不可见；

模块脚本自动采用严格模式；

模块中，可使用import命令加载其他模块（.js后缀不可省，需提供绝对或相对 URL），也可用export命令输出对外接口；

模块中，顶层this关键字返回undefined，而不是指向window。即在模块顶层使用this关键字，是无意义的；

同一模块如果加载多次，将只执行一次。



## 二 ES6 与 CommonJS 模块的差异

### 两个重大差异：

**CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用**。
**CommonJS 模块是运行时加载，ES6 模块是编译时输出接口**。

第二个差异是因为 CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。

### ES6 模块的运行机制与 CommonJS 不一样：

JS 引擎对脚本静态分析时，遇到**ES6模块加载命令import，就会生成一个只读引用**。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。

**ES6 的import有点像 Unix 系统的“符号连接”，原始值变了，import加载的值也会跟着变。因此，ES6 模块是动态引用，并且不会缓存值**，模块里面的变量绑定其所在的模块。

由于 ES6 输入的模块变量，只是一个“符号连接”，所以这个变量是只读的，对它进行重新赋值会报错。

**export通过接口，输出的是同一个值。不同的脚本加载这个接口，得到的都是同样的实例**。

例子略，具体可参考最下面的链接。

## 三 Node 中加载 ES6 模块

**Node 对 ES6 模块的处理**较麻烦，因为它有自己的 CommonJS 模块格式，与 ES6 模块格式不兼容。**目前的解决方案是，将两者分开，ES6 模块和 CommonJS 采用各自的加载方案**。

**Node 要求 ES6 模块采用.mjs后缀文件名**。只要脚本文件里使用import或export，就必须用.mjs后缀。**require命令不能加载.mjs文件**，会报错，只有import命令才可以加载.mjs文件。

这项功能还在试验阶段。安装 Node v8.5.0 或以上版本，可能要用--experimental-modules参数才能打开该功能。



```
$ node --experimental-modules my-app.mjs
```



为了与浏览器的import加载规则相同，Node 的.mjs文件支持 URL 路径。



```
import './foo?query=1'; // 加载 ./foo 传入参数 ?query=1
```



上面代码中，脚本路径带有参数?query=1，Node 会按 URL 规则解读。**同一个脚本只要参数不同，就会被加载多次，并且保存成不同的缓存**。由于这个原因，只要文件名中含有:、%、#、?等特殊字符，最好对这些字符进行转义。

目前，Node 的import命令只支持加载本地模块（file:协议），不支持加载远程模块。

如果模块名不含路径，那么import命令会去node_modules目录寻找这个模块。


最后，**Node 的import命令是异步加载，这与浏览器的处理方法相同**。

### 内部变量
ES6 模块应该是通用的，同一个模块不用修改，就可以用在浏览器环境和服务器环境。为了达到这个目标，**Node 规定 ES6 模块之中不能使用 CommonJS 模块的特有的一些内部变量**。

首先是this关键字。**ES6 模块之中，顶层的this指向undefined；CommonJS 模块的顶层this指向当前模块，这是两者的一个重大差异**。

其次，以下这些顶层变量在 ES6 模块之中都是不存在的。

arguments
require
module
exports
__filename
__dirname


### ES6 模块加载 CommonJS 模块
CommonJS 模块的输出都定义在module.exports这个属性上面。**Node 的import命令加载 CommonJS 模块，Node 会自动将module.exports属性，当作模块的默认输出**，即等同于export default xxx。

CommonJS 模块的输出缓存机制，在 ES6 加载方式下依然有效。


## 四 循环加载
### 1. 什么是循环加载？
**“循环加载”指：a脚本的执行依赖b脚本，而b脚本的执行又依赖a脚本**。

“循环加载”表示存在强耦合，如处理不好，可能导致递归加载，使程序无法执行，因此应避免出现。

但实际上很难避免，尤其是**依赖关系复杂的大项目，很容易出现a依赖b，b依赖c，c又依赖a的情况。故模块加载机制必须考虑“循环加载”**的情况。

CommonJS 和 ES6，处理“循环加载”的方法不同，返回结果也不同。

CommonJS模块加载的原理参考[CommonJS规范](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qi-ta-ji-chu/commonjsgui-fan.md)。

### 2. CommonJS 模块的循环加载处理
**CommonJS 模块是加载时执行，即脚本代码在require时，就全部执行。一旦出现某模块被"循环加载"，就只输出已经执行的部分，还未执行的部分不会输出**。

CommonJS 输入的是被输出值的拷贝，不是引用。

另外，由于 **CommonJS 模块遇到循环加载时，返回的是当前已经执行的部分的值，而不是代码全部执行后的值，两者可能会有差异**。所以，通过模块输入变量时，必须非常小心。

### 3. ES6 模块的循环加载处理
ES6 模块是**动态引用**，如果**用import从一模块加载变量，那些变量不会被缓存，而是成为指向被加载模块的引用，需开发者自己保证，真正取值时能取到值**。

ES6 循环加载处理的例子：

```
// a.mjs
import {bar} from './b';
console.log('a.mjs');
console.log(bar);
export let foo = 'foo';

// b.mjs
import {foo} from './a';
console.log('b.mjs');
console.log(foo);
export let bar = 'bar';
```

首先，执行a.mjs以后，引擎发现它加载了b.mjs，因此会优先执行b.mjs，然后再执行a.js。接着，执行b.mjs的时候，已知它从a.mjs输入了foo接口，这时不会去执行a.mjs，而是认为这个接口已经存在了，继续往下执行。执行到第三行console.log(foo)的时候，才发现这个接口根本没定义，因此报错。

解决这个问题的方法，是让b.mjs运行时，foo已经有定义了。可通过将foo写成函数来解决。

```
// a.mjs
import {bar} from './b';
console.log('a.mjs');
console.log(bar());
function foo() { return 'foo' }
export {foo};

// b.mjs
import {foo} from './a';
console.log('b.mjs');
console.log(foo());
function bar() { return 'bar' }
export {bar};
```

这时再执行a.mjs就可以得到预期结果。



```
$ node --experimental-modules a.mjs
b.mjs
foo
a.mjs
bar
```


这是因为函数具有提升作用，在执行`import {bar} from './b'`时，函数foo就已经有定义了，所以b.mjs加载时候不会报错。这也意味着，如把函数foo改成函数表达式，也会报错。


## 五 ES6 模块的转码

浏览器目前还不完全支持 ES6 模块（特别是低版本的浏览器），为了现在就能使用，可将ES6代码转为 ES5 的写法。除了 [Babel](https://babeljs.io/) 可用来转码外，还有[ES6 module transpiler](https://github.com/esnext/es6-module-transpiler)和 [SystemJS](https://github.com/systemjs/systemjs) 两个方法。

SystemJS。是一个垫片库（polyfill），可在浏览器内加载 ES6 模块、AMD 模块和 CommonJS 模块，将其转为 ES5 格式。它在后台调用的是 Google 的 Traceur 转码器。


## 参考
http://es6.ruanyifeng.com/#docs/module-loader

