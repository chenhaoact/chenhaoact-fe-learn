# js原型、原型继承与非ES6的面向对象编程

## 一 对象封装

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

**"构造函数"，就是一个普通函数，但内部使用了this变量。对构造函数使用new运算符，就能生成实例，且this变量会绑定在实例对象上。**


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





## 参考 

### 未学习

Javascript 面向对象编程（一）：封装
http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html

Javascript面向对象编程（二）：构造函数的继承
http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html

Javascript面向对象编程（三）：非构造函数的继承
http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html

从__proto__和prototype来深入理解JS对象和原型链
https://github.com/creeperyang/blog/issues/9