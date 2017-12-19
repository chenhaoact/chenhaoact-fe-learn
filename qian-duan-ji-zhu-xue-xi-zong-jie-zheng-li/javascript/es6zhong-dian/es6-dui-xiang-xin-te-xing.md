# ES6 对象新特性

## 一 基本的一些新特性
### 2 属性名表达式 
ES5 定义对象的属性，有两种方法。



```
// 方法一：直接用标识符作为属性名，属性名定死
obj.foo = true;

// 方法二：用表达式作属性名（属性名可为变量），要将表达式放在方括号之内
obj['a' + 'bc'] = 123;
```



但**如果使用字面量方式定义对象（使用大括号），在 ES5 中只能使用方法一，表达式里写表达式的方法无法用，也就不能指定属性名为变量**。



```
var obj = {
  foo: true,
  abc: 123
};
```



**ES6 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内**。



```
let propKey = 'foo';

let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
};
```

这就是ES6的属性名表达式。



## 二 新增的常用方法

### 1. Object.assign() 将所有可枚举属性的值从一或多个源对象 复制 到目标对象。返回目标对象。

**常用于拷贝对象的值生成新对象。**

**特别注意，对象的复制一律不要用 = （用=给的是引用，会混乱），要用 Object.assign()！**

```
Object.assign(target, ...sources)
```

参数：  
target 目标对象  
sources   (多个)源对象。

返回值：   
目标对象。

例子


```
var obj = { a: 1 };
var copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
copy === obj   // false
```

具体参考：
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign

### 2. Object.freeze(obj)
冻结一个对象。
冻结指的是不能向这个对象添加新的属性，不能修改其已有属性的值，不能删除已有属性，以及不能修改该对象已有属性的可枚举性、可配置性、可写性。
也就是说，这个对象永远是不可变的。该方法返回被冻结的对象。


```
export const objA = {
 a:'A'
}

Object.freeze(objA); 
```




