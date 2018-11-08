## 对象新增的常用方法
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
const target = { a: 1 };

const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

#### 注意点：
* Object.assign方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。

#### Object.assign方法的常见用途
* 为对象添加属性、方法
* 克隆对象
* 合并多个对象
* 为属性指定默认值

具体参考：
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign

### 2. Object.freeze(obj) 冻结一个对象，返回被冻结的对象
**冻结指不能向这个对象添加新的属性，不能修改其已有属性的值，不能删除已有属性，以及不能修改该对象已有属性的可枚举性、可配置性、可写性**。

也就是说，**这个对象永远是不可变的**。

```
export const objA = {
 a:'A'
}

Object.freeze(objA); 
```

### Object.getPrototypeOf() 从子类上获取父类



```
Object.getPrototypeOf(ColorPoint) === Point
// true
```


**可用这个方法判断，一个类是否继承了另一个类**。



