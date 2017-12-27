# Module 的语法及使用

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

**import命令具有提升效果**，会提升到整个模块的头部，首先执行。这种行为的本质是，**import命令是编译阶段执行的，在代码运行之前**。

from指定模块文件位置，可以是相对路径，也可以是绝对路径，.js后缀可省略（其他类型后缀不能省）。如只是模块名，不带有路径，那么必须有配置文件，告诉 Js 引擎该模块的位置(如webpack的别名配置)。

```
import {myMethod} from 'util';
```


#### （2）使用as关键字将输入变量重命名

```
import { lastName as surname } from './profile';

```

#### （3）import是静态执行，所以不能使用表达式，变量，语句等只有在运行时才能得到结果的语法结构。另外因它在静态解析阶段执行，所以它是模块中最早执行的，最好不要把CommonJS 模块的require和 ES6 模块的import写在同一个模块，可能不会得到预期结果

```

// 报错
import { 'f' + 'oo' } from 'my_module';

// 报错
let module = 'my_module';
import { foo } from module;

// 报错
if (x === 1) {
  import { foo } from 'module1';
} else {
  import { foo } from 'module2';
}
```


上面三种写法都报错，因它们用到了表达式、变量和if结构。**在静态分析阶段，这些语法都是没法得到值**的。

#### （4）import语句会执行所加载的模块

```
import 'lodash';
```

上面代码**仅仅执行模块，但不输入任何值**。

如多次重复执行同一句import语句，那么只会执行一次，而不会执行多次：



```
import 'lodash';
import 'lodash';
```

上面代码加载了两次lodash，但是**只会执行一次**。

import { foo } from 'my_module';
import { bar } from 'my_module';

// 等同于
import { foo, bar } from 'my_module';

上面代码虽然foo和bar**不同的变量在两个语句中加载，但它们对应的是同一个my_module实例（也是只执行一次**）。即import语句是 [Singleton（单例）模式](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/javascript/jsshe-ji-mo-shi/dan-ti-ff08-singleton-ff09-mo-shi-ff08-dan-li-mo-shi-ff09.md)。

### 3. 模块的整体加载 （*）
可以**用星号（*）指定一个对象，所有输出值都加载在这个对象上面**。

下面是一个circle.js文件，它输出两个方法area和circumference。

```
// circle.js
export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```

逐一指定要加载的写法：



```
// main.js
import { area, circumference } from './circle';

console.log('圆面积：' + area(4));
console.log('圆周长：' + circumference(14));

```



**整体加载的写法**如下：



```
import * as circle from './circle';

console.log('圆面积：' + circle.area(4));
console.log('圆周长：' + circle.circumference(14));
```

注意，**模块整体加载所在的那个对象**（上例是circle），**应该是可静态分析的**，所以**不允许运行时改变**，如：

```
import * as circle from './circle';

// 下面两行都是不允许的
circle.foo = 'hello';
circle.area = function () {};
```

### 4. export default 命令 （输出默认模块）
前面例子使用import命令时，用户需知道所要加载的变量或函数名，否则无法加载。

**为给用户提供方便，让他们不用阅读文档（无需知道所要加载的变量名或函数名）就能加载模块，就要用到export default命令，为模块指定默认输出**。



```
// export-default.js
export default function () {
  console.log('foo');
}
```



上面代码是一个模块文件export-default.js，它的默认输出是一个匿名函数。

**其他模块加载该模块时，import命令可以为该匿名函数指定任意名字**。

```
// import-default.js
import customName from './export-default';
customName(); // 'foo'
```



上面代码的import命令，可以用任意名称指向export-default.js输出的方法，这时就不需要知道原模块输出的函数名。注意，**这时import命令后面，不使用大括号**。

export default命令用在非匿名函数前，也是可以的。



```
// export-default.js
export default function foo() {
  console.log('foo');
}

// 或写成
function foo() {
  console.log('foo');
}

export default foo;
```


上面代码中，**因为前面用了export default，foo函数的函数名foo，在模块外部是无效的。加载的时候，视同匿名函数加载**。

默认输出和正常输出的比较：

使用export default时，对应的import语句不需要使用大括号；不使用export default时，对应的import语句需使用大括号。

export default命令用于指定模块的默认输出。显然，**一个模块只能有一个默认输出，因此export default命令只能使用一次**。所以，import命令后才不用加大括号，因为只可能对应一个方法。

本质上，export default就是输出一个叫做default的变量或方法，然后系统允许你为它取任意名字。所以它后面不能跟变量声明语句。

// 正确
export var a = 1;

// 正确
var a = 1;
export default a;

// 错误
export default var a = 1;

上面代码中，**export default a的含义是将变量a的值赋给变量default。所以，最后一种写法会报错**。


有了export default命令，输入模块时就非常直观了，以输入 lodash 模块为例。



```
import _ from 'lodash';
```



如想在一条import语句中，同时输入默认方法和其他接口，可以写成：


```
import _, { each, each as forEach } from 'lodash';
```

对应上面代码的export语句如下。

export default function (obj) {
  // ···
}

export function each(obj, iterator, context) {
  // ···
}

export { each as forEach };

上面代码的最后一行的意思是，暴露出forEach接口，默认指向each接口，即forEach和each指向同一个方法。

**export default也可以用来输出类**。

```
// MyClass.js
export default class { ... }

// main.js
import MyClass from 'MyClass';
let o = new MyClass();
```

### 5. export 与 import 的复合写法 （export 和 from写在一行）
如果一个模块之中，先输入后输出同一个模块，import语句可以与export语句写在一起。

export { foo, bar } from 'my_module';

// 等同于
import { foo, bar } from 'my_module';
export { foo, bar };

上面代码，**export和import语句可以结合在一起，就有了 export 和 from写在一行的写法**。

**模块的接口改名和整体输出，就可以采用这种写法**。

// 接口改名
export { foo as myFoo } from 'my_module';

// 整体输出
export * from 'my_module';

### 6. 模块的继承
**模块之间也可以继承。先把要继承的模块全部引入并用*导出，再修改一些变量，将自定义的变量导出（就会覆盖继承模块的对应变量）**。

假设circleplus模块，继承了circle模块。

// circleplus.js
export * from 'circle';

export var e = 2.71828182846;
export default function(x) {
  return Math.exp(x);
}

上面代码中的export *，表示再输出circle模块的所有属性和方法。注意，export * 命令会忽略circle模块的default方法。然后，上面代码又输出了自定义的e变量和默认方法。

### 7. 跨模块常量（优化项目结构与复用性，可读性）
const声明的常量只在当前代码块有效。如果想设置跨模块的常量（即跨多个文件），或者说**一个值要被多个模块共享，可以采用下面的写法（定义constants.js 模块，专门存放常量**）。



```
// constants.js 模块
export const A = 1;
export const B = 3;


// test1.js 模块
import * as constants from './constants';
console.log(constants.A); // 1
console.log(constants.B); // 3
```




如果**要使用的常量非常多，可以建一个专门的constants目录，将各种常量写在不同的文件里面，保存在该目录下**。

```
// constants/db.js
export const db = {
  url: 'http://my.couchdbserver.local:5984',
  admin_username: 'admin',
  admin_password: 'admin password'
};

// constants/user.js
export const users = ['root', 'admin', 'staff', 'ceo', 'chief', 'moderator'];
```


然后，**将这些文件输出的常量，合并在index.js里**。


```
// constants/index.js
export {db} from './db';
export {users} from './users';
```



**使用的时候，直接加载index.js**：



```
// script.js
import {db, users} from './index';
```



### 8. import()

**import命令会被 Js 引擎静态分析**，先于模块内的其他模块执行（叫做”连接“更合适），故无法使用变量，表达式，语句等。这样的设计，**固然有利于编译器提高效率，但也导致无法在运行时加载模块**。在语法上，条件加载就不可能实现。**如果import命令要取代 Node 的require方法，这就形成了一个障碍**。因为**require是运行时加载模块**，**import命令无法取代require的动态加载功能**。



```
const path = './' + fileName;
const myModual = require(path);
```



上面的语句就是**动态加载**，**即**require**到底加载哪一个模块，只有运行时才知道**。import语句做不到这一点。

因此，有一个[提案](https://github.com/tc39/proposal-dynamic-import)，建议**引入import()函数，完成动态加载**。

import(specifier)
上面代码中，import函数的参数specifier，指定所要加载的模块的位置。import命令能够接受什么参数，import()函数就能接受什么参数，两者区别主要是后者为动态加载。

**import()返回一个 Promise 对象**。下面是一个例子。



```
const main = document.querySelector('main');

import(`./section-modules/${someVariable}.js`)
  .then(module => {
    module.loadPageInto(main);
  })
  .catch(err => {
    main.textContent = err.message;
  });
```


  
**import()函数可以用在任何地方，不仅仅是模块，非模块的脚本也可以使用。它是运行时执行，即，什么时候运行到这一句，也会加载指定的模块**。另外，import()函数与所加载的模块**没有静态连接关系**，这点也与import语句不同。

**import()类似于 Node 的require方法，区别主要是前者是异步加载，后者是同步加载**。

#### （1）import()的一些适用场合。

**a. 按需加载。在需要的时候，再加载某个模块**



```
button.addEventListener('click', event => {
  import('./dialogBox.js')
  .then(dialogBox => {
    dialogBox.open();
  })
  .catch(error => {
    /* Error handling */
  })
});
```



上面代码中，import()方法放在click事件的监听函数之中，只有用户点击了按钮，才会加载这个模块。



**b. 条件加载,可以放在if代码块，根据不同的情况，加载不同的模块**

if (condition) {
  import('moduleA').then(...);
} else {
  import('moduleB').then(...);
}
上面代码中，如果满足条件，就加载模块 A，否则加载模块 B。

c. **动态的模块路径**

import()允许模块路径动态生成。

import(f())
.then(...);

上面代码中，根据函数f的返回结果，加载不同的模块。

#### （2）import()的注意点:
**import()加载模块成功以后，这个模块会作为一个对象，当作then方法的参数**。因此，**可使用对象解构赋值语法，获取输出接口**。



```
import('./myModule.js')
.then(({export1, export2}) => {
  // ...·
});
```



上面代码，export1和export2都是myModule.js的输出接口，可以解构获得。

如果模块有**default输出接口，可以用参数直接获得**。



```
import('./myModule.js')
.then(myModule => {
  console.log(myModule.default);
});
```





如果**想同时加载多个模块，可采用下面的写法**。



```
Promise.all([
  import('./module1.js'),
  import('./module2.js'),
])
.then(([module1, module2]) => {
   ···
});
```




**import()也可用在 async 函数中**。



```
async function main() {
  const myModule = await import('./myModule.js');
  const {export1, export2} = await import('./myModule.js');
  const [module1, module2, module3] =
    await Promise.all([
      import('./module1.js'),
      import('./module2.js'),
      import('./module3.js'),
    ]);
}
main();
```

