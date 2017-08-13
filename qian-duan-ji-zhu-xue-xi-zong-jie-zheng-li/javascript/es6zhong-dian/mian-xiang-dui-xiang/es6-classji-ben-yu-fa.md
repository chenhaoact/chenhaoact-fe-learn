# ES6 class基本语法

## 一 简介 
### 1. 类的基本写法
JS中，生成实例对象的传统方法是通过构造函数。

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

注意，定义“类”的方法时，前面不需要加function关键字，直接把函数定义放进去即可。另外，方法间不需要逗号分隔。

### 2. ES6 的类，完全可以看作构造函数的另一种写法

```
class Point {  // ... }

typeof Point // "function"
Point === Point.prototype.constructor // true

```


代码表明，**类的数据类型是函数**，**类本身就指向构造函数。**

### 3. 类生成实例
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

### 4. 构造函数的prototype属性，在 ES6 的“类”中继续存在。类的所有方法都定义在类的prototype属性上



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

**在类的实例上面调用方法，其实就是调用原型上的方法。**



```
class B {}
let b = new B();

b.constructor === B.prototype.constructor // true
```


### 5. 由于类的方法都定义在prototype对象上，所以类的新方法可以添加在prototype对象上；Object.assign方法可以很方便地一次向类添加多个新方法



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


### 7. 类内部所有定义的方法，都是不可枚举的（non-enumerable）



## 参考

### 已学习


### 待学习
[Class 的基本语法(阮一峰《ES6标准入门》)](http://es6.ruanyifeng.com/#docs/class)

目前只过了简介部分

[深入浅出ES6（十三）：类 Class](http://www.infoq.com/cn/articles/es6-in-depth-classes)

