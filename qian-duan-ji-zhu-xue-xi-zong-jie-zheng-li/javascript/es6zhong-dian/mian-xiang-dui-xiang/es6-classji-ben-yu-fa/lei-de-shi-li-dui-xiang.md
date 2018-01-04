## 类的实例对象
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


