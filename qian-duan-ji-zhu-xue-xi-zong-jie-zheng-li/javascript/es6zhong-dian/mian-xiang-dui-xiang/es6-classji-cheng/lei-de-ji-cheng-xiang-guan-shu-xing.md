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



