## 简介
**Class 可通过extends关键字实现继承**，这**比 ES5 通过修改原型链实现继承清晰方便**很多。

```
class Point {
}

class ColorPoint extends Point {
}

```

上面代码定义了ColorPoint类，该类**通过extends关键字，继承父类的所有属性和方法**。

在ColorPoint这个**子类内部再加上它自己的代码**。



```
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}

```

### 1. super关键字

上面代码，constructor和toString方法都出现了**super关键字，它表示父类的构造函数，用来新建父类的this对象**。

**子类必须在constructor方法中调用super方法，否则新建实例时会报错**。**因为子类没有自己的this对象，而是继承父类的this对象，然后对其加工**。
因为**子类实例的构建，是基于对父类实例加工，子类的构造函数中，只有调用super方法后才能返回父类实例，才可使用this关键字，否则报错**。

#### 注意：super关键字，既可当作函数使用（代表父类的构造函数），也可当对象使用（在普通方法中，指向父类的原型对象；在静态方法中，指向父类）。两种情况下，用法完全不同，具体使用见 [super关键字](http://es6.ruanyifeng.com/#docs/class-extends#super-关键字)


### 2. ES6 继承的实质
**ES5 的继承，实质是先创造子类的实例对象this，再将父类方法添加到this上**（Parent.apply(this)）。

**而 ES6 的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this**。

若子类没定义constructor方法，此方法会被默认添加。


### 3. 生成子类实例 （子类实例同时是子类和父类的实例）
下面是**生成子类实例的代码**。

```
let cp = new ColorPoint(25, 8, 'green');

cp instanceof ColorPoint // true
cp instanceof Point // true
```


上面代码，**实例对象cp同时是ColorPoint和Point两个类的实例，这与 ES5 一致**。

### 4. 父类的静态方法，也会被子类继承 （静态方法 前面加static的方法，只是不会被实例继承，但能被子类继承）



```
class A {
  static hello() {
    console.log('hello world');
  }
}

class B extends A {
}

B.hello()  // hello world
```



上面代码，hello()是A类的静态方法，B继承A，也继承了A的静态方法。










