## 一 基本的一些规范
### 1. 块级作用域与常量变量（const与let）
####（1）**let 取代 var**
**var命令存在变量提升效用，let命令没有**这个问题。



```
if (true) {
  console.log(x); // ReferenceError
  let x = 'hello';
}
```


如使用**var**替代let，console.log那一行就不会报错，而会输出undefined，因为**变量声明提升到代码块的头部。违反了变量先声明后使用的原则**。

#### （2）全局常量和线程安全
**let和const，优先使用const，尤其是全局环境，不应设置变量，只应设置常量const**

**const优于let有几个原因**：
1. const可提醒阅读程序的人，这个变量不应改变，也防止了无意间修改变量值所导致的错误；
2. const比较符合函数式编程思想，运算不改变值，只是新建值，这样也有利于将来的分布式运算；
3. **Js 编译器会对const进行优化，所以多用const，有利于提高程序的运行效率**，let和const的本质区别，其实是编译器内部的处理不同。



```
// bad
var a = 1, b = 2;

// good
const a = 1;
const b = 2;

// best
const [a, b] = [1, 2];
```

所有的函数都应该设置为常量。

长远看，Js 可能会有多线程的实现，这时**let表示的变量，只应出现在单线程运行的代码中**，不能是多线程共享的，这样**有利于保证线程安全**。


### 2. 解构赋值

**使用数组成员对变量赋值，优先使用解构赋值**。

```
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

**函数的参数如果是对象的成员，优先使用解构赋值**。

```
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
}

// best
function getFullName({ firstName, lastName }) {
  // 里边可以直接使用firstName, lastName
}
```


如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值。便于以后添加返回值，以及更改返回值顺序。

### 3. 对象

#### （1）对象尽量静态化，一旦定义，不得随意添加新的属性。如果添加属性不可避免，使用Object.assign


```

// bad
const a = {};
a.x = 3;

// 如果添加属性不可避免，用Object.assign()
const a = {};
Object.assign(a, { x: 3 });

// good
const a = { x: null };
a.x = 3;
```

#### （2）如对象的属性名是动态的，可在创造对象时，使用属性表达式


```
// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```


上面代码，对象obj最后一个属性名，需计算得到。这时最好采用属性表达式，在新建obj时，将该属性与其他属性定义在一起。这样**所有属性就在一个地方定义了**。

### 4. 数组
#### （1）使用扩展运算符（...）拷贝数组

```
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

#### （2）使用 Array.from 方法，将类似数组的对象转为数组



```
const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```

### 5. 函数
#### （1）立即执行函数可写成箭头函数的形式



```
(() => {
  console.log('Welcome');
})();
```



#### （2）需使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了 this



```
// bad
[1, 2, 3].map(function (x) {
  return x * x;
});

// good
[1, 2, 3].map((x) => {
  return x * x;
});
```

#### （3）箭头函数取代Function.prototype.bind，不应再用 self/_this/that 绑定 this



```
// bad
const self = this;
const boundMethod = function(...params) {
  return method.apply(self, params);
}

// best
const boundMethod = (...params) => method.apply(this, params);
```


####（4）简单的、单行的、不会复用的函数，建议采用箭头函数。如函数体较复杂，行数较多，还应采用传统函数写法

#### （5）所有配置项都应该集中在一个对象，放在最后一个参数，布尔值不可以直接作为参数

// bad
function divide(a, b, option = false ) {
}

// good
function divide(a, b, { option = false } = {}) {
}


不要在函数体内使用 arguments 变量，使用 rest 运算符（...）代替。因为 rest 运算符显式表明你想要获取参数，而且 arguments 是一个类似数组的对象，而 rest 运算符可以提供一个真正的数组。

// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
使用默认值语法设置函数参数的默认值。

// bad
function handleThings(opts) {
  opts = opts || {};
}

// good
function handleThings(opts = {}) {
  // ...
}




## 二 具体参考
Airbnb 公司的 JavaScript 风格规范
https://github.com/airbnb/javascript

es6入门-阮一峰
http://es6.ruanyifeng.com/#docs/style