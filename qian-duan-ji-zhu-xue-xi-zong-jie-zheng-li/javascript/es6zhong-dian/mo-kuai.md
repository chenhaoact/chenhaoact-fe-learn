# 模块Module

## 一 简介
ES6之前，Js 一直没有模块（module）体系，对开发大型、复杂项目形成了巨大障碍。

社区制定了一些模块加载方案，主要有 **CommonJS 和 AMD。前者用于服务器，后者用于浏览器**。

**ES6** 在语言标准上，实现了**模块功能，成为浏览器和服务器通用的模块解决方案**。

### 1. ES6 Module和 commonjs、AMD的对比
#### （1）静态化
**ES6 模块的设计思想，是尽量静态化，编译时就能确定模块的依赖关系，及输入和输出的变量**。**CommonJS 和 AMD 模块，都只能在运行时确定这些**。

比如CommonJS的加载为“运行时加载”，只有运行时才能得到这个对象，导致完全没办法在编译时做“静态优化”。

ES6的import，不能“动态”拼一个路径，因为ES6的模块化就是**强制静态化**。

**ES6 模块不是对象，而是通过export命令显式指定输出的代码，再通过import命令输入**。



```
// ES6模块
import { stat, exists, readFile } from 'fs';
```



上面代码实质是从fs模块加载 3 个方法，其他方法不加载。

这种加载**称为“编译时加载”或静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 高**。

由于 ES6 模块是**编译时加载，使得静态分析成为可能**。有了它，就能进一步拓宽 Js 的语法，如引入宏（macro）和**类型检验**（type system）这些只能靠静态分析实现的功能。


附：如果还是要动态引入模块：
如要动态引入模块，建议用node(commonjs)的require。require动态引入模块路径 require()里直接放url变量会报错: Cannot find module "."， 可先加带.的路径前缀的字符串再+文件路径变量即可，如：

```
const MdUrl = 'data/' + this.props.params.id + '.md';
const MdHtml = require('../../' + MdUrl);
```

import和require的对比参考：
Node中没搞明白require和import，你会被坑的很惨
http://www.tuicool.com/articles/uuUVBv2

#### （2）ES6 模块的好处

1. 静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 高。

2.。编译时加载，使得**静态分析**成为可能。能实现**类型检验这些只能靠静态分析实现的功能。**

**除了静态加载带来的各种好处，ES6 模块还有以下好处：**

3. 不再需要UMD模块格式，将来**服务器和浏览器都会支持 ES6 模块格式**。目前通过工具库其实已做到。
**将来浏览器的新 API 就能用模块格式提供，不再必须做成全局变量或者navigator对象的属性，这样会更加灵活**。

4. 不再需要对象作为命名空间（如Math对象），未来这些功能可以通过模块提供。


## 二 语法
ES6 模块自动采用[严格模式](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/javascript/jszhong-dian-zheng-li/yan-ge-mo-shi.md)，不管有没有在模块头部加"use strict";。

其中，尤其需注意this的限制。**ES6 模块中，顶层的this指向undefined，即不应该在顶层代码使用this**。

### 1. export 命令 
#### （1）基本写法，输出变量
export命令用于规定模块的对外接口，即：允许输出模块。

**一个模块就是一个独立的文件**。
**该文件内部所有变量，外部无法获取。如希望外部能读取模块内的某个变量，就必须使用export关键字输出该变量**。

如：

```
// profile.js
export var firstName = 'Michael';
```

#### （2）使用 {} 导出多个变量（推荐的写法）
export的写法，除像上面这样，还有另一种。



```
var firstName = 'Michael';
var lastName = 'Jackson';

export {firstName, lastName};
```

使用大括号指定所要输出的一组变量。它与前一种写法（直接放置在var语句前）等价，但应优先考虑使用这种写法。因为**这样可以在脚本尾部，一眼看清楚输出了哪些变量**。

#### （3）输出函数或类（class）

export命令除了输出变量，还可以输出函数或类（class）。

```
export function multiply(x, y) {

};
```


上面代码对外输出函数multiply。

#### （4）使用as关键字重命名
export输出的变量是本来的名字，但可使用as关键字重命名。


```

function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

上面代码使用as关键字，重命名了函数v1和v2的对外接口。重命名后，v2可以用不同的名字输出两次。

#### （5）特别注意：export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系



```
// 报错
export 1;

// 报错
var m = 1;
export m;
```

上面写法报错因为没有提供对外的接口。第一种写法直接输出 1，第二种写法通过变量m，还是直接输出 1。1只是一个值，不是接口。

正确的写法：

// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};

上面三种正确写法都规定了对外的接口m。其他脚本可以通过这个接口，取到值1。它们的实质是，在接口名与模块内部变量之间，建立了一一对应的关系。

同样function和class的输出，也必须遵守这样的写法：

```
// 报错
function f() {}
export f;

// 正确
export function f() {};

// 正确
function f() {}
export {f};
```



#### （6）export语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可取到模块内部实时的值，这一点与 CommonJS 完全不同。CommonJS 模块输出的是值的缓存，不存在动态更新

```
export var foo = 'bar';
setTimeout(() => foo = 'baz', 500);
```

上面代码输出变量foo，值为bar，500 毫秒之后变成baz。



#### （7）export命令可出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错

import命令也是如此。因为**处于条件代码块 （ {} ）之中，就没法做静态优化了，违背了 ES6 模块的设计初衷**。



```
function foo() {
  export default 'bar' // SyntaxError
}
foo()
```



上面代码，export语句放函数中，报错。

### 2. import 命令
import命令用于输入其他模块提供的功能，即：导入模块。

使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。

#### （1）基本写法

```
// main.js
import {firstName, lastName, year} from './profile';
```

上面代码的import命令，用于加载profile.js文件，并从中输入变量。import命令接受一对大括号，里面指定要从其他模块导入的变量名。**大括号里面的变量名，必须与被导入模块（profile.js）对外接口的名称相同**。

后面的from指定模块文件的位置，可以是相对路径，也可以是绝对路径，.js后缀可以省略。如果只是模块名，不带有路径，那么必须有配置文件，告诉 JavaScript 引擎该模块的位置。

import {myMethod} from 'util';
上面代码中，util是模块文件名，由于不带有路径，必须通过配置，告诉引擎怎么取到这个模块。


#### （2）使用as关键字将输入变量重命名

```
import { lastName as surname } from './profile';

```




### 如何在浏览器和 Node 之中，加载 ES6 模块？




