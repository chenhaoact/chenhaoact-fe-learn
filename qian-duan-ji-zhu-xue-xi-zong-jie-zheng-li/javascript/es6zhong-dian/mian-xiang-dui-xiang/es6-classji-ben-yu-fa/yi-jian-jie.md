# 简介
**JS在ES6之前，生成实例对象的传统方法是通过构造函数 （定义一个函数模拟构造函数，该函数首字母大写，通过此函数生成实例对象）**。

**例子（重要）**：


```
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

ES6 提供更接近其他语言（如java）的写法，引入了 Class（类），作为对象的模板。通过**class关键字，可以定义类。**

ES6 的class可看作只是一个语法糖，绝大部分功能，ES5 都可做到，**新的class写法只是让对象原型的写法更清晰、更像面向对象编程的语法**而已。

**使用class定义类：**

```
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

constructor方法是构造方法，而this关键字则代表实例对象。**ES5 的构造函数**Point，**对应 ES6 的** Point **类的构造方法**。

### 这里使用new 类方法 生成实例对象时传入的参数
这些参数会被constructor函数（在实例对象初始时就会执行）接收到（这里传入了x，y），然后通过constructor里的this.x = x;把该参数的绑定到this（即实例对象本身）上，这样实例对象在调用类的方法（如这里的toString()）时，就可以通过this.x拿到值。


注意，定义“类”的方法时，前面不需要加function关键字，直接把函数定义放进去即可。另外，方法间不需要逗号分隔。

