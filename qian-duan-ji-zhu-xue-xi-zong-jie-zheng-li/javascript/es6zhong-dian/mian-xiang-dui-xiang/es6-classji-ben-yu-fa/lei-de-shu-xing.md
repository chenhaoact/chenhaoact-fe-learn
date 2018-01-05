## 类的属性
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

**该提案中，类的实例属性可以用等式，写入类的定义之中**。可以不在constructor方法里定义，更清晰。**而类的静态属性只要在上面的实例属性写法前面，加上static**关键字。

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

### 5. new.target 属性
new是从构造函数生成实例对象的命令。
**ES6** 为new命令**引入了new.target属性，用在构造函数中，返回new命令作用于的那个构造函数**。**如构造函数不是通过new命令调用，new.target返回undefined**，因此此属性**可用来确定构造函数是怎么调用的**。**Class 内调用new.target，返回当前 Class**。



```
function Person(name) {
  if (new.target !== undefined) {
    this.name = name;
  } else {
    throw new Error('必须使用 new 命令生成实例');
  }
}

// 另一种写法
function Person(name) {
  if (new.target === Person) {
    this.name = name;
  } else {
    throw new Error('必须使用 new 命令生成实例');
  }
}

var person = new Person('张三'); // 正确
var notAPerson = Person.call(person, '张三');  // 报错
```



上面代码确保构造函数只能通过new命令调用。

**Class 内调用new.target，返回当前 Class：**



```
class Rectangle {
  constructor(length, width) {
    console.log(new.target === Rectangle);
    this.length = length;
    this.width = width;
  }
}

var obj = new Rectangle(3, 4); // 输出 true
```


注意，**子类继承父类时，new.target会返回子类：**



```
class Rectangle {
  constructor(length, width) {
    console.log(new.target === Rectangle);
    // ...
  }
}

class Square extends Rectangle {
  constructor(length) {
    super(length, length);
  }
}

var obj = new Square(3); // 输出 false
```


上面代码，new.target会返回子类。

**利用这个特点，可写出不能独立使用（不能实例化）、必须继承后才能使用的类：**



```
class Shape {
  constructor() {
    if (new.target === Shape) {
      throw new Error('本类不能实例化');
    }
  }
}

class Rectangle extends Shape {
  constructor(length, width) {
    super();
    // ...
  }
}

var x = new Shape();  // 报错
var y = new Rectangle(3, 4);  // 正确
```


上面代码，Shape类不能被实例化，只能用于继承。

注意，**在函数外使用new.target会报错**。



