# ES6 class基本语法

## 一 简介

JS中，**生成实例对象的传统方法是通过构造函数**。

如：


```
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

ES6 提供更接近其他语言（如java）的写法，引入了 Class（类），作为对象的模板。通过**class关键字，可以定义类。**

ES6 的class可看作只是一个语法糖，绝大部分功能，ES5 都可做到，**新的class写法只是让对象原型的写法更清晰、更像面向对象编程的语法**而已。

**使用class定义类：**

```
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

constructor方法是构造方法，而this关键字则代表实例对象。**ES5 的构造函数**Point，**对应 ES6 的** Point **类的构造方法**。

### 这里使用new 类方法 生成实例对象时传入的参数
这些参数会被constructor函数（在实例对象初始时就会执行）接收到（这里传入了x，y），然后通过constructor里的this.x = x;把该参数的绑定到this（即实例对象本身）上，这样实例对象在调用类的方法（如这里的toString()）时，就可以通过this.x拿到值。


注意，定义“类”的方法时，前面不需要加function关键字，直接把函数定义放进去即可。另外，方法间不需要逗号分隔。

## 二 基本使用与注意点

### 1. ES6 类的数据类型是函数，类本身就指向构造函数

ES6 的类，完全可以看作构造函数的另一种写法：

```
class Point {  // ... }

typeof Point // "function"
Point === Point.prototype.constructor // true

```

上面代码表明，类的数据类型就是函数，类本身就指向构造函数。

### 2. 类生成实例
使用时直接对类使用new命令，跟构造函数用法一致。

```
class Bar {
  doStuff() {
    console.log('stuff');
  }
}

var b = new Bar();
b.doStuff() // "stuff"
```

### 3. 构造函数的prototype属性，在 ES6 的“类”中继续存在。类的所有方法都定义在类的prototype属性上



```
class Point {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }

  toValue() {
    // ...
  }
}
```

等同于：

```
Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
};
```

### 4. 在类的实例上面调用方法，其实就是调用原型上的方法



```
class B {}
let b = new B();

b.constructor === B.prototype.constructor // true
```


### 5. 由于类的方法都定义在prototype对象上，所以类的新方法可添加在prototype对象上；Object.assign方法能很方便地一次向类添加多个新方法



```
class Point {
  constructor(){
    // ...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});
```



### 6. prototype对象的constructor属性，直接指向“类”本身，这与 ES5 一致



```
Point.prototype.constructor === Point // true

```


### 7. 类内部所有定义的方法，都是不可枚举的（non-enumerable），这点与 ES5 不一致

### 8. 类的属性名，可采用表达式



```
let methodName = 'getArea';

class Square {
  constructor(length) {
    // ...
  }

  [methodName]() {
    // ...
  }
}
```

上面代码，Square类的方法名getArea，是从表达式得到的。

### 9. 严格模式
ES6类和模块内部，默认就是严格模式，所以不需使用use strict指定运行模式。

考虑到未来所有的代码，其实都运行在模块之中，所以 **ES6 实际上把整个语言升级到了严格模式**。

### 10. 类（方法）必须使用new调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行


## 三 类的 constructor 方法

类的默认方法，通**过new命令生成对象实例时，自动调用该方法**；
如果没有显式定义，一个空的constructor方法会被默认添加；
constructor方法默认返回实例对象（即this），可以指定返回另外一个对象，但会导致实例对象不是该类实例；



```
class Point {
  constructor() {}
}
```



## 四 类的实例对象

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

### 五 Class 表达式



## 参考
http://es6.ruanyifeng.com/#docs/class

MDN-Classes
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes

[深入浅出ES6（十三）：类 Class](http://www.infoq.com/cn/articles/es6-in-depth-classes)

