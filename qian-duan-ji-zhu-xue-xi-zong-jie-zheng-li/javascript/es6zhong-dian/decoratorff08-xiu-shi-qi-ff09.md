# Decorator（修饰器）
## 一 简介
许多面向对象语言都有修饰器（Decorator）函数，**用来修改类的行为（可以修改类的行为，也可以修改类的属性和方法的行为）**，简单的说，就是**通过@符号+特定的字符 定义代码中类的一系列行为（@符号的修饰器函数和其行为是可以自定义的）**。

目前，有一个[提案](https://github.com/tc39/proposal-decorators)将这项功能，引入了 ECMAScript。

### 1. 用途
**用来修改类的行为（可以修改类的行为，也可以修改类的属性和方法的行为）**；

除了**注释**，修饰器**还能用来类型检查**。对于类来说，这项功能相当有用。**长期来看，它将是 JS 代码静态分析的重要工具**；

修饰器只能用于类和类的方法，不能用于单独的函数，因为存在函数提升。

## 二 类的修饰

修饰器的行为基本是下面这样：



```
@decorator
class A {}

// 等同于

class A {}
A = decorator(A) || A;
```


即：修饰器是一个对类进行处理的函数。修饰器函数的第一个参数，就是所要修饰的目标类。



```
function testable(target) {
  // ...
}
```


上面代码中，testable函数的参数target，就是会被修饰的类。如果觉得一个参数不够用，可在修饰器外再封装一层函数。


注意：**修饰器对类的行为的改变，是代码编译时发生的，而不是在运行时**。这意味着，修饰器能在编译阶段运行代码。即：**修饰器本质是编译时执行的函数**。


## 三 方法的修饰

### 1. 修饰器不仅可以修饰类，还可以修饰类的属性（比如类的某个方法）

例子：

```
class Person {
  @readonly
  name() { return `${this.first} ${this.last}` }
}
```
修饰器readonly用来修饰“类”的name方法。

修饰器函数readonly一共可以接受三个参数。



```
function readonly(target, name, descriptor){
  // descriptor对象原来的值如下
  // {
  //   value: specifiedFunction,
  //   enumerable: false,
  //   configurable: true,
  //   writable: true
  // };
  descriptor.writable = false;
  return descriptor;
}

readonly(Person.prototype, 'name', descriptor);
// 类似于
Object.defineProperty(Person.prototype, 'name', descriptor);

```

**修饰器函数的第一个参数是类的原型对象**，上例是Person.prototype，修饰器本意是要“修饰”类的实例，但这时实例还没生成，所以只能去修饰原型（这不同于类的修饰，那种情况target参数指类本身）；**第二个参数是所要修饰的属性名，第三个参数是该属性的描述对象**。

上面代码还说明，修饰器（readonly）会修改属性的描述对象（descriptor），然后被修改的描述对象再用来定义属性。


### 2. 修饰器有注释的作用



```
@testable
class Person {
  @readonly
  @nonenumerable
  name() { return `${this.first} ${this.last}` }
}
```

上面代码一眼就能看出，Person类可测试，而name方法只读和不可枚举。

下面是使用 Decorator 写法的组件，看上去一目了然。



```
@Component({
  tag: 'my-component',
  styleUrl: 'my-component.scss'
})
export class MyComponent {
  @Prop() first: string;
  @Prop() last: string;
  @State() isVisible: boolean = true;

  render() {
    return (
      <p>Hello, my name is {this.first} {this.last}</p>
    );
  }
}
```


### 3. 如果同一个方法有多个修饰器，会像剥洋葱一样，先从外到内进入，然后由内向外执行



```
function dec(id){
  console.log('evaluated', id);
  return (target, property, descriptor) => console.log('executed', id);
}

class Example {
    @dec(1)
    @dec(2)
    method(){}
}
// evaluated 1
// evaluated 2
// executed 2
// executed 1

```


上面代码，外层修饰器@dec(1)先进入，但内层修饰器@dec(2)先执行。


## 四 修饰器相关的js类库和技术

### 1. [core-decorators.js](https://github.com/jayphelps/core-decorators)

一个第三方模块，提供了一些常见的修饰器。

Popular with React/Angular, but is framework agnostic.

#### 提供的一些修饰器
@autobind 
使方法中的this对象，绑定原始对象

@readonly
使属性或方法不可写

@override
检查子类的方法，是否正确覆盖父类的同名方法，不正确会报错

@deprecate (别名@deprecated)
在控制台显示一条警告，表示该方法将废除

@suppressWarnings
抑制deprecated修饰器导致的console.warn()调用。异步代码发出的调用除外

## 五 Mixin
在**修饰器基础上，可实现Mixin模式**。

**Mixin模式，是对象继承的一种替代方案，中文译为“混入”，意为在一个对象中混入另外一对象的方法**。

例子



```
const Foo = {
  foo() { console.log('foo') }
};

class MyClass {}

Object.assign(MyClass.prototype, Foo);

let obj = new MyClass();
obj.foo() // 'foo'
```

上面代码，对象Foo有foo方法，**通过Object.assign，可将foo方法“混入”MyClass类，导致其实例obj对象都具有foo方法。这就是“混入”模式的一个简单实现**。

下面，部署一个通用脚本mixins.js，将 Mixin 写成一个修饰器。



```
export function mixins(...list) {
  return function (target) {
    Object.assign(target.prototype, ...list);
  };
}
```


然后，可使用上面这个修饰器，为类“混入”各种方法。

```
import { mixins } from './mixins';

const Foo = {
  foo() { console.log('foo') }
};

@mixins(Foo)
class MyClass {}

let obj = new MyClass();
obj.foo() // "foo"
```


通过mixins这个修饰器，实现了在MyClass类上面“混入”Foo对象的foo方法。

但**上面的方法会改写MyClass类的prototype对象，如不喜欢这点，也可通过类的继承实现 Mixin**。



```
class MyClass extends MyBaseClass {
  /* ... */
}
```


上面代码，MyClass继承了MyBaseClass。**如想在MyClass里“混入”一个foo方法，一个办法是在MyClass和MyBaseClass之间插入一混入类，这个类有foo方法，并继承了MyBaseClass的所有方法，然后MyClass再继承这个类**。



```
let MyMixin = (superclass) => class extends superclass {
  foo() {
    console.log('foo from MyMixin');
  }
};
```



上面代码中，MyMixin是一个混入类生成器，接受superclass作为参数，然后返回一个继承superclass的子类，该子类包含一个foo方法。

接着，目标类再去继承这个混入类，就达到了“混入”foo方法的目的。



```
class MyClass extends MyMixin(MyBaseClass) {
  /* ... */
}

let c = new MyClass();
c.foo(); // "foo from MyMixin"
```


如果需要“混入”多个方法，就生成多个混入类。



```
class MyClass extends Mixin1(Mixin2(MyBaseClass)) {
  /* ... */
}
```


**这种写法的一个好处，是可以调用super，因此可以避免在“混入”过程中覆盖父类的同名方法**。



```
let Mixin1 = (superclass) => class extends superclass {
  foo() {
    console.log('foo from Mixin1');
    if (super.foo) super.foo();
  }
};

let Mixin2 = (superclass) => class extends superclass {
  foo() {
    console.log('foo from Mixin2');
    if (super.foo) super.foo();
  }
};

class S {
  foo() {
    console.log('foo from S');
  }
}

class C extends Mixin1(Mixin2(S)) {
  foo() {
    console.log('foo from C');
    super.foo();
  }
}
```


上面代码中，每一次混入发生时，都调用了父类的super.foo方法，导致父类同名方法没被覆盖，行为被保留下来。

```
new C().foo()
// foo from C
// foo from Mixin1
// foo from Mixin2
// foo from S
```


## 六 Trait 
**Trait 也是一种修饰器，效果与 Mixin 类似，但是提供更多功能，比如防止同名方法的冲突、排除混入某些方法、为混入的方法起别名等等**。

[traits-decorator](https://github.com/CocktailJS/traits-decorator)这个第三方模块提供一些traits修饰器，不仅可以接受对象，还可以接受 ES6 类作为参数。

## 七 Babel 转码器的支持
目前，Babel 转码器已支持 Decorator。

首先，安装babel-core和babel-plugin-transform-decorators。由于后者包括在babel-preset-stage-0之中，所以改为安装babel-preset-stage-0亦可。



```
$ npm install babel-core babel-plugin-transform-decorators
```


然后，**设置配置文件.babelrc（plugins里加了transform-decorators）**。



```
{
  "plugins": ["transform-decorators"]
}
```


这时，Babel 就可以对 Decorator 转码了。

脚本中打开的命令如下。



```
babel.transform("code", {plugins: ["transform-decorators"]})
```



Babel 的官方网站提供一个[在线转码器](https://babeljs.io/repl/)，只要勾选 Experimental，就能支持 Decorator 的在线转码。


## 参考
http://es6.ruanyifeng.com/#docs/decorator
