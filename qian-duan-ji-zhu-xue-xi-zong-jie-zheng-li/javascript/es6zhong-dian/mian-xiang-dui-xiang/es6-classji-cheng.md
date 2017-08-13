# ES6 class继承

## 简介
**Class 可通过extends关键字实现继承**，这**比 ES5 通过修改原型链实现继承清晰方便**很多。



```
class Point {
}

class ColorPoint extends Point {
}

```

上面代码定义了一个ColorPoint类，该类通过extends关键字，继承了Point类的所有属性和方法。

再在ColorPoint内部加上它自己的代码。

class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}

上面代码中，constructor和toString方法都出现了**super关键字，它表示父类的构造函数，用来新建父类的this对象**。

**子类必须在constructor方法中调用super方法，否则新建实例时会报错**。这是**因为子类没有自己的this对象，而是继承父类的this对象，然后对其加工**。在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则报错。因为子类实例的构建，是基于对父类实例加工，只有super方法才能返回父类实例。

ES5 的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。

**ES6 的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this**。

若子类没定义constructor方法，此方法会被默认添加。


下面是**生成子类实例的代码**。



```
let cp = new ColorPoint(25, 8, 'green');

cp instanceof ColorPoint // true
cp instanceof Point // true
```



上面代码中，**实例对象cp同时是ColorPoint和Point两个类的实例，这与 ES5 一致**。

## 参考

### 已学习


### 待学习
[Class 的继承（阮一峰《ES6标准入门》）](http://es6.ruanyifeng.com/#docs/class-extends)

目前只过了简介部分
