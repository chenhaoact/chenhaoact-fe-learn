## 基本使用与注意点

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

### 11. 类不存在变量提升，必须先定义才能使用，这点与 ES5 不同

```
new Foo(); // ReferenceError
class Foo {}
```

上面代码，Foo类使用在前，定义在后，这样会报错，因为 **ES6 不会把类的声明提升到代码头部**。这种**规定的原因与继承有关，必须保证子类在父类之后定义**。


