# js原型、原型继承与非ES6的面向对象编程

## 一 对象封装与原型

JS是一种基于对象的语言，遇到的所有东西几乎都是对象。但**在ES6之前**它并不是一种真正的面向对象编程（OOP）语言，因为语法中没有class（类）。

ES6之前，要**把"属性"和"方法"，封装成一个对象，甚至从原型对象生成一个实例对象，有下列做法**：

### 1. 原始模式-生成生成实例对象

写一个函数，解决生成对象代码重复的问题。

```
function Cat(name,color) {
　　　　return {
　　　　　　name:name,
　　　　　　color:color
　　　　}
　　}
```

生成实例对象，就等于是在调用函数：

```
var cat1 = Cat("大毛","黄色");
var cat2 = Cat("二毛","黑色");
```

问题：cat1和cat2之间没有内在联系，不能反映出是同一个原型对象的实例。

### 2. 构造函数模式

**"构造函数"，就是一个普通函数（函数名首字母大写！），但内部使用了this变量。对构造函数使用new运算符，就能生成实例，且this变量会绑定在实例对象上。**


原型对象 实例：
```
function Cat(name,color){
　　　　this.name=name;
　　　　this.color=color;
　　}
```

生成实例对象：

```
var cat1 = new Cat("大毛","黄色");
var cat2 = new Cat("二毛","黑色");
alert(cat1.name); // 大毛
alert(cat1.color); // 黄色
```

**用 new 构造函数 生成的实例对象会自动含有constructor属性，指向其构造函数。**

```
　　alert(cat1.constructor == Cat); //true
　　alert(cat2.constructor == Cat); //true
```


**JS的instanceof运算符，可验证原型对象（这里就是构造函数）与实例对象之间的关系：**　　

```
alert(cat1 instanceof Cat); //true
```

问题：
存在浪费内存问题。
对每一个实例对象，**共同属性和方法**都一样，**每次生成实例，却必须重复，多占用了内存。**

```
function Cat(name,color){
　　　　this.name = name;
　　　　this.color = color;
　　　　this.type = "猫科动物"; //共同属性
　　　　this.eat = function(){alert("吃老鼠");}; //共同方法
　　}
```

**更好的做法是让公共属性和方法在内存中只生成一次，然后所有实例都指向那个内存地址，于是就有了Prototype模式（原型模式）。**

### 3. Prototype模式（原型模式）

#### （1） Prototype（原型的定义） ！重点！
**JS的每个构造函数（注意是构造函数！）都有一个prototype属性，指向另一个对象（其所有属性和方法，都会被构造函数的实例继承）。**

**可以把共同的属性和方法，直接定义在prototype对象上。**

```
function Cat(name,color){
　　　　this.name = name;
　　　　this.color = color;
　　}
　　Cat.prototype.type = "猫科动物";
　　Cat.prototype.eat = function(){alert("吃老鼠")};
```

生成实例：

```
var cat1 = new Cat("大毛","黄色");
　　var cat2 = new Cat("二毛","黑色");
　　alert(cat1.type); // 猫科动物
　　cat1.eat(); // 吃老鼠
```

这时**所有实例的共同属性和方法**（type属性和eat()方法），**都是同一个内存地址，指向prototype对象，提高了运行效率**。

```
alert(cat1.eat == cat2.eat); //true
```

#### （2）prototype属性的相关辅助方法

**isPrototypeOf()**
判断某个proptotype对象和某个实例之间的关系。

```
alert(Cat.prototype.isPrototypeOf(cat1)); //true
```

**hasOwnProperty()**
判断某一个属性是本地属性，还是继承自prototype对象。

```
alert(cat1.hasOwnProperty("name")); // true
```

**in运算符**
a. **判断某实例是否有某属性，不管是不是本地属性**。

```
alert("name" in cat1); // true

```

b. **in运算符还可遍历某对象所有属性**:

```
for(var prop in cat1) { alert("cat1["+prop+"]="+cat1[prop];
}
```

## 二 构造函数的继承

### 1. 用prototype模式（常见）

例：

现有"动物"对象的构造函数：

```
　　function Animal(){
　　　　this.species = "动物";
　　}

```

还有"猫"对象的构造函数：

```
　　function Cat(name,color){
　　　　this.name = name;
　　　　this.color = color;
　　}

```

怎样才能使"猫"继承"动物"？

使用prototype模式：

"猫"的prototype对象，指向一个Animal的实例，那么所有"猫"的实例，就能继承Animal：

```　　
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;

var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物

```

第一行，将Cat的prototype对象指向一个Animal的实例。
　
第二行，由于任何一prototype对象都有constructor属性，指向其构造函数。加了"Cat.prototype = new Animal();"这一行后，Cat.prototype.constructor指向Animal（原来是Cat）。

每一个实例也有constructor属性，默认调用prototype对象的constructor属性。因此实例cat1.constructor也指向Animal！
　
**这会导致继承链的紊乱（实例cat1明明是用构造函数Cat生成的）**，因此必须手动纠正，将Cat.prototype对象的constructor值改为Cat（第二行，很重要，编程时务必要遵守）。

**即时刻遵守：**
**如果替换了prototype对象，下一步必然是为新的prototype对象加上constructor属性，指回原来的构造函数**：

```
o.prototype = ... ;
o.prototype.constructor = o;
```

## 二 非构造函数的继承

例：
现在有一对象"中国人"。


```
　　var Chinese = {
　　　　nation:'中国'
　　};
```

还有一对象"医生"。


```
　　var Doctor ={
　　　　career:'医生'
　　}

```

怎样才能让"医生"去继承"中国人"，生成"中国医生"的对象？
这**两个对象都是普通对象，不是构造函数，无法使用构造函数方法实现"继承"**。

### 方法1：使用object()方法

object()方法

```
function object(o) {
　　　　function F() {}
　　　　F.prototype = o;
　　　　return new F();
　　}
```

这个object()函数把子对象的prototype属性，指向父对象

使用时，第一步，在父对象基础上，生成子对象：

```
　　var Doctor = object(Chinese);

```

再加上子对象本身的属性：


```
　　Doctor.career = '医生';

```

这时，子对象已经继承了父对象的属性：


```
　　alert(Doctor.nation); //中国
```

### 方法2 把父对象的属性，全部拷贝给子对象，也能实现继承。

#### 浅拷贝（不建议）
这样的拷贝有一个问题：如果父对象的属性等于数组或另一个对象，子对象获得的只是一个内存地址，而不是真正拷贝，因此存在父对象被篡改的可能。

只能拷贝基本类型的数据，这种拷贝叫做"浅拷贝"。

#### 深拷贝（建议）
**"深拷贝"**，就是能**实现真正意义上的数组和对象的拷贝**。它的实现只要**递归调用"浅拷贝"**就行了。

```
function deepCopy(p, c) {
　　　　var c = c || {};
　　　　for (var i in p) {
　　　　　　if (typeof p[i] === 'object') {
　　　　　　　　c[i] = (p[i].constructor === Array) ? [] : {};
　　　　　　　　deepCopy(p[i], c[i]);
　　　　　　} else {
　　　　　　　　　c[i] = p[i];
　　　　　　}
　　　　}
　　　　return c;
　　}
```

使用：


```
　　var Doctor = deepCopy(Chinese);

```


## 参考 

### 已学习
Javascript 面向对象编程（一）：封装
http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html

Javascript面向对象编程（二）：构造函数的继承
http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html

Javascript面向对象编程（三）：非构造函数的继承
http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html

### 未学习
从__proto__和prototype来深入理解JS对象和原型链
https://github.com/creeperyang/blog/issues/9