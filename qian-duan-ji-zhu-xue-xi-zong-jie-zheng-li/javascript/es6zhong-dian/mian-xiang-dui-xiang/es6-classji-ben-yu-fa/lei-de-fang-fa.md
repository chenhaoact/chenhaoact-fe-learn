## 类的方法

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

