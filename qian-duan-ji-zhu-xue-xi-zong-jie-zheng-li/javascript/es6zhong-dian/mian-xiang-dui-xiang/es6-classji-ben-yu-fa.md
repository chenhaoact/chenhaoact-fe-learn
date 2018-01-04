# ES6 class基本语法

## 一 [简介](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/javascript/es6zhong-dian/mian-xiang-dui-xiang/es6-classji-ben-yu-fa/yi-jian-jie.md)

## 二 [基本使用与注意点](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/javascript/es6zhong-dian/mian-xiang-dui-xiang/es6-classji-ben-yu-fa/ji-ben-shi-yong-yu-zhu-yi-dian.md)


## 三 类的实例对象

### 1. 生成类的实例对象（与 ES5 一样，使用new命令）



```
class Point {
  // ...
}

// 报错
var point = Point(2, 3);

// 正确
var point = new Point(2, 3);
```

### 2. 实例的属性除非显式定义在其本身（即定义在this对象上），否则都定义在原型上（即定义在class上）。

这点与 ES5 一样。


```
//定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true

```

上面代码中，x和y都是实例对象point自身的属性（因为**定义在this变量上），hasOwnProperty方法返回true**，

而**toString是原型对象的属性（因为定义在Point类上），所以hasOwnProperty方法返回false**。

### 3. 类的所有实例共享一个原型对象


```
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__ === p2.__proto__
//true
```

上面代码中，p1和p2都是Point**类的不同实例，原型都是Point.prototype，所以__proto__属性相等**。

因此可通过实例的__proto__属性为“类”添加方法。
**__proto__ 并不是语言本身的特性，是各大厂商具体实现时添加的私有属性**，虽然目前很多现代浏览器的 JS 引擎中都提供了这个私有属性，但依旧**不建议在生产使用该属性，避免对环境产生依赖。生产环境可使用Object.getPrototypeOf 方法来获取实例对象的原型，然后再来为原型添加方法/属性**。



```
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__.printName = function () { return 'Oops' };

p1.printName() // "Oops"
p2.printName() // "Oops"

var p3 = new Point(4,2);
p3.printName() // "Oops"
```


上面代码在p1原型上添加了printName方法，由于**所有实例共享同一个原型**，因此p2也可以调用这个方法。此后新建的实例p3也可以调用这个方法。这意味着，**使用实例的__proto__属性改写原型，必须相当谨慎，不推荐使用，因为这会改变“类”的原始定义，影响到所有实例**。

## 四 类的属性
### 1. 定义类的属性
定义属性，一般是在constructor中通过this.属性名 = 传入参数值，指定初始值，后面各个函数里 可以this.属性名拿到属性并进行赋值。

### 2. Class 的静态属性和实例属性
**静态属性：指 Class 本身的属性，即Class.propName，而非定义在实例对象（this）上的属性**。



```
class Foo {
}

Foo.prop = 1;
Foo.prop // 1
```



**上面的写法（类外边用类.属性名 = 值）为类定义了一个静态属性**prop。

**目前，只有这种写法可行，因为 ES6 明确规定，Class 内部只有静态方法，没有静态属性（属性前加static无效）**。



```
// 以下两种写法都无效
class Foo {
  // 写法一
  prop: 2

  // 写法二
  static prop: 2
}

Foo.prop // undefined
```



目前**有一个[静态属性的提案](https://github.com/tc39/proposal-class-fields)，对实例属性和静态属性都规定了新的写法**。

**该提案中，类的实例属性可以用等式，写入类的定义之中**。



```
class MyClass {
  myProp = 42;
而目前，定义实例属性，只能写在类的constructor方法里。

class ReactCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
}
上面代码中，构造方法constructor里面，定义了this.state属性。

有了新的写法以后，可以不在constructor方法里面定义。

class ReactCounter extends React.Component {
  state = {
    count: 0
  };
}
这种写法比以前更清晰。

为了可读性的目的，对于那些在constructor里面已经定义的实例属性，新写法允许直接列出。

class ReactCounter extends React.Component {
  state;
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
}
（2）类的静态属性

类的静态属性只要在上面的实例属性写法前面，加上static关键字就可以了。

class MyClass {
  static myStaticProp = 42;

  constructor() {
    console.log(MyClass.myStaticProp); // 42
  }
}
同样的，这个新写法大大方便了静态属性的表达。

// 老写法
class Foo {
  // ...
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
上面代码中，老写法的静态属性定义在类的外部。整个类生成以后，再生成静态属性。这样让人很容易忽略这个静态属性，也不符合相关代码应该放在一起的代码组织原则。另外，新写法是显式声明（declarative），而不是赋值处理，语义更好。



### 3. 私有属性
与私有方法一样，ES6 **暂不支持**私有属性。目前，**有一个[提案](https://github.com/tc39/proposal-private-methods)**，为class加了私有属性。方法是**在属性名之前加#表示私有属性**。



```
class Point {
  #x;

  constructor(x = 0) {
    #x = +x; // 写成 this.#x 亦可
  }

  get x() { return #x }
  set x(value) { #x = +value }
}
```

之所以**引入新的前缀#表示私有属性，而没采用private关键字，是因为 JS 是一门动态语言，使用独立的符号似乎是唯一的可靠方法，能够准确地区分**一种属性是否为私有属性。Ruby 用@表私有属性，ES6 使用了#，是因为@已被留给了Decorator。

**该提案只规定了私有属性的写法。但是它实际上也可用来写私有方法**。

### 4. name 属性
**本质上，ES6 的类只是 ES5 的构造函数的一层包装，所以函数的许多特性都被Class继承，包括name属性**。



```
class Point {}
Point.name // "Point"
```

name属性：总返回紧跟在class关键字后面的类名。



## 五 类的方法
### 1. 类的 constructor 方法

类的默认方法，通**过new命令生成对象实例时，自动调用该方法**；
如果没有显式定义，一个空的constructor方法会被默认添加；
constructor方法默认返回实例对象（即this），可以指定返回另外一个对象，但会导致实例对象不是该类实例；



```
class Point {
  constructor() {}
}
```
### 2.Class 的静态方法 （static）
**类相当于实例的原型，所有在类中定义的方法，都会被实例继承。在一方法前，加static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这称为“静态方法”。**



```
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```


上面代码，Foo类的classMethod方法前有static关键字，表明是静态方法，可直接在Foo类上调用，而不能在Foo类的实例上调用。

注意，**如静态方法包含this关键字，这个this指类，而非实例对象**。



```
class Foo {
  static bar () {
    this.baz();
  }
  static baz () {
    console.log('hello');
  }
  baz () {
    console.log('world');
  }
}

Foo.bar() // hello
```


上面代码，静态方法bar调用了this.baz，这里的this指的是Foo类，而不是Foo的实例，等同于调用Foo.baz。另外，从例子还可看出，**静态方法可以与非静态方法重名**。

**父类的静态方法，可以被子类继承**：



```
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
}

Bar.classMethod() // 'hello'
```

上面代码，父类Foo有一个静态方法，子类Bar可调用这个方法。

**静态方法也可从super对象上调用**：

```
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
  static classMethod() {
    return super.classMethod() + ', too';
  }
}

Bar.classMethod() 
```

### 3. 私有方法
**私有方法是常见需求，但 ES6 不提供，只能通过变通方法模拟实现**。

方法一： 在命名上加以区别（不推荐）
方法前加下划线，表示这是一个只限于内部使用的私有方法。但不保险，在类外部，还是可以调用这个方法。

方法二：将私有方法移出模块，因为模块内部的所有方法都是对外可见的。公有方法里调用类外边的私有方法。（推荐）



```
class Widget {
  foo (baz) {
    bar.call(this, baz);
  }

  // ...
}

function bar(baz) {
  return this.snaf = baz;
}
```


上面代码，**foo是公有方法(bar是私有方法)，公有方法foo内部调用了bar.call(this, baz)**。这使得bar实际上成为了当前模块的私有方法。


方法三：**利用Symbol值的唯一性，将私有方法的名字命名为一个Symbol值**。

```
const bar = Symbol('bar');
const snaf = Symbol('snaf');

export default class myClass{

  // 公有方法
  foo(baz) {
    this[bar](baz);
  }

  // 私有方法
  [bar](baz) {
    return this[snaf] = baz;
  }

  // ...
};
上面代码中，
```

bar和snaf都是**Symbol值，导致第三方无法获取到它们，因此达到了私有方法和私有属性的效果**。

### 4. 取值函数（getter）和存值函数（setter）
与 ES5 一样，在**“类”的内部可使用get和set关键字，对某属性设置存值函数和取值函数，拦截该属性的存取行为（ 这时定义属性值就不是在constructor中通过this.属性名 = 传入参数值，而是通过 get 属性名() 和 set 属性名() 自定义设值和取值行为 ）**。



```
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

上面代码中，prop属性有对应的存值函数和取值函数，因此赋值和读取行为都被自定义了。

**存值函数和取值函数设置在属性的 Descriptor 对象上**。可通过Object.getOwnPropertyDescriptor()方法拿到。

### 5. Class 的 Generator 方法 
类的某个方法前加星号（*），就表示该方法是一个 Generator 函数。



```
class Foo {
  constructor(...args) {
    this.args = args;
  }
  * [Symbol.iterator]() {
    for (let arg of this.args) {
      yield arg;
    }
  }
}

for (let x of new Foo('hello', 'world')) {
  console.log(x);
}
// hello
// world

```

上面代码，Foo类的Symbol.iterator方法前有一个星号，表示该方法是一个 Generator 函数。Symbol.iterator方法返回一个Foo类的默认遍历器，for...of循环会自动调用这个遍历器。

## 六 Class 表达式
与函数一样，类也可以使用表达式的形式定义。



```
const MyClass = class Me {
  getClassName() {
    return Me.name;
  }
};
```

上面代码用表达式定义类。注意，**这个类的名字是MyClass而不是Me**，**Me只在 Class 内部代码可用**，指代当前类。

如果类的内部没用到的话，可以省略Me，写成下面的形式。

```
const MyClass = class { /* ... */ };
```

采用 Class 表达式，可写出立即执行的 Class实例。 


## 七 this 的指向
**类的方法内部如果含有this，它默认指向类的实例**。但须非常小心，一旦单独使用该方法，很可能报错。



```
class Logger {
  printName(name = 'there') {
    this.print(`Hello ${name}`);
  }

  print(text) {
    console.log(text);
  }
}

const logger = new Logger();
const { printName } = logger;
printName(); // TypeError: Cannot read property 'print' of undefined
```



上面代码，printName方法中的this，默认指向Logger类的实例。但如果**将这个方法提取出来单独使用，this会指向该方法运行时所在的环境**，因找不到print方法而报错。

解决方法一（最简单）：在类的构造方法中绑定this



```
class Logger {
  constructor() {
    this.printName = this.printName.bind(this);
  }

  // ...
}
```



方法二：使用箭头函数（自动绑定this）



```
class Logger {
  constructor() {
    this.printName = (name = 'there') => {
      this.print(`Hello ${name}`);
    };
  }

  // ...
}
```



方法三：使用Proxy，获取方法时，自动绑定this。



```
function selfish (target) {
  const cache = new WeakMap();
  const handler = {
    get (target, key) {
      const value = Reflect.get(target, key);
      if (typeof value !== 'function') {
        return value;
      }
      if (!cache.has(value)) {
        cache.set(value, value.bind(target));
      }
      return cache.get(value);
    }
  };
  const proxy = new Proxy(target, handler);
  return proxy;
}

const logger = selfish(new Logger());
```

## 八 

## 参考
http://es6.ruanyifeng.com/#docs/class

MDN-Classes
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes

[深入浅出ES6（十三）：类 Class](http://www.infoq.com/cn/articles/es6-in-depth-classes)

