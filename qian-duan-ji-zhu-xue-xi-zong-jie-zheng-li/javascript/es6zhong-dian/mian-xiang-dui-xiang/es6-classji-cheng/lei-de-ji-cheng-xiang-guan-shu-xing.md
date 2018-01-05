## 类的继承相关属性
### 1. 类的 prototype 属性和__proto__属性 （）
**多数浏览器的 ES5 实现中，每个对象都有`__proto__`属性，指向对应的构造函数的prototype属性**。

**Class 作为构造函数的语法糖，同时有prototype属性和`__proto__`属性，因此同时存在两条继承链**。

（1）**子类**的**`__proto__`属性，表示构造函数的继承，总是指向父类**。

（2）子类**prototype属性的`__proto__`属性，表示方法的继承，总是指向父类的prototype属性**。



```
class A {
}

class B extends A {
}

B.__proto__ === A // true
B.prototype.__proto__ === A.prototype // true
```


上面代码，子类B的`__proto__`属性指向父类A，子类B的prototype属性的`__proto__`属性指向父类A的prototype属性。

#### 这两条继承链，可以这样理解（重要）：
**`__proto__`属性是原型（本质是类），prototype属性是原型对象（本质是原型类的实例对象）。作为一个对象，子类（B）的原型（`__proto__`属性）是父类（A）；作为一个构造函数，子类（B）的原型对象（prototype属性）是父类的原型对象（prototype属性）的实例**。

```
Object.create(A.prototype);
// 等同于
B.prototype.__proto__ = A.prototype;
```

#### 例子：extends 的继承目标不同对应的 `__proto__` 和 prototype

extends关键字后可跟多种类型的值。

```
class B extends A {
}
```

上面代码的A，只要是一个有prototype属性的函数，就能被B继承。由于函数都有prototype属性（除了Function.prototype函数），因此A可以是任意函数。

会有**三种特殊情况**：

**第一种：子类继承Object类**



```
class A extends Object {
}

A.__proto__ === Object // true
A.prototype.__proto__ === Object.prototype // true
```



这种情况下，A其实就是构造函数Object的复制，A的实例就是Object的实例。

**第二种，不存在任何继承**



```
class A {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === Object.prototype // true
```


这种情况，A作为一个基类（即不存在任何继承），就是一个普通函数，所以直接继承Function.prototype。但是，A调用后返回一个空对象（即Object实例），所以A.prototype.__proto__指向构造函数（Object）的prototype属性。

**第三种，子类继承null**



```
class A extends null {
}

A.__proto__ === Function.prototype // true
A.prototype.__proto__ === undefined // true
```


这种情况与第二种情况非常像。A也是一个普通函数，所以直接继承Function.prototype。但是，A调用后返回的对象不继承任何方法，所以它的__proto__指向Function.prototype，即实质上执行了下面的代码。



```
class C extends null {
  constructor() { return Object.create(null); }
}
```


实例的 __proto__ 属性
子类实例的__proto__属性的__proto__属性，指向父类实例的__proto__属性。也就是说，子类的原型的原型，是父类的原型。



```
var p1 = new Point(2, 3);
var p2 = new ColorPoint(2, 3, 'red');

p2.__proto__ === p1.__proto__ // false
p2.__proto__.__proto__ === p1.__proto__ // true
```


上面代码中，ColorPoint继承了Point，导致前者原型的原型是后者的原型。

因此，通过子类实例的__proto__.__proto__属性，可以修改父类实例的行为。



```
p2.__proto__.__proto__.printName = function () {
  console.log('Ha');
};

p1.printName() // "Ha"
```


上面代码在ColorPoint的实例p2上向Point类添加方法，结果影响到了Point的实例p1。



