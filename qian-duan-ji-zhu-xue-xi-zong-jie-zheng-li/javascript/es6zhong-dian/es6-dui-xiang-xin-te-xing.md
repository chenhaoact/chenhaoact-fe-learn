# ES6 对象新特性

## 一 常用方法

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




