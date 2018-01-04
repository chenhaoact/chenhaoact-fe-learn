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

**该提案中，类的实例属性可以用等式，写入类的定义之中**。



```
class MyClass {
  myProp = 42;
而目前，定义实例属性，只能写在类的constructor方法里。

class ReactCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
}
上面代码中，构造方法constructor里面，定义了this.state属性。

有了新的写法以后，可以不在constructor方法里面定义。

class ReactCounter extends React.Component {
  state = {
    count: 0
  };
}
这种写法比以前更清晰。

为了可读性的目的，对于那些在constructor里面已经定义的实例属性，新写法允许直接列出。

class ReactCounter extends React.Component {
  state;
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
}
（2）类的静态属性

类的静态属性只要在上面的实例属性写法前面，加上static关键字就可以了。

class MyClass {
  static myStaticProp = 42;

  constructor() {
    console.log(MyClass.myStaticProp); // 42
  }
}
同样的，这个新写法大大方便了静态属性的表达。

// 老写法
class Foo {
  // ...
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
上面代码中，老写法的静态属性定义在类的外部。整个类生成以后，再生成静态属性。这样让人很容易忽略这个静态属性，也不符合相关代码应该放在一起的代码组织原则。另外，新写法是显式声明（declarative），而不是赋值处理，语义更好。



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



