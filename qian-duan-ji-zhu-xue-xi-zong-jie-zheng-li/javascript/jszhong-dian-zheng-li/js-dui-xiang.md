# js 对象

## 一 对象基础

### （1）获取属性值的两种方式：对象.属性名 和 对象[属性名]

{属性名:属性值} 以及 对象.属性名中，属性名不能是变量，而**对象[属性名] 中属性名可以是变量，该方式有时候会更灵活和强大。
**


### （2）对象之间的比较

#### a.判断对象字面属性与值是否相等

基本类型string,number通过值来比较，而对象（Date,Array）及普通对象**通过指针指向的内存中的地址来做比较**。用===是判断不出来仅仅字面的属性和值相等的对象的。

Underscore和**LoDash有一个名为_.isEqual()方法**，可用来**比较好的处理深度对象的比较（定义时候字面属性及值相等就会返回true）**。

参考：
Javascript 判断对象是否相等
http://www.zuojj.com/archives/775.html

#### b.数组中是否包含某对象（仅字面属性和值匹配）

不用 数组.includes()或者 数组.indexOf()  (只能用到字符或数值等基础类型的包含判断)
用 loadsh 的 _.findIndex()

```
let arrA = [{a:1,b:2},{b:1,c:1}];


_.findIndex(arrA,{a:1,b:2}) // 0
_.findIndex(arrA,{b:1,c:1}) // 1
_.findIndex(arrA,{a:1,b:1}) // -1
```

### （3）js 对象的浅拷贝和深拷贝

[javascript中的深拷贝和浅拷贝？
](https://www.zhihu.com/question/23031215)

[JavaScript中的浅拷贝和深拷贝
](https://segmentfault.com/a/1190000008637489)

**数组里增加对象要注意**：

**对象的值相当于其引用，不能直接赋值，那样会指向同一个对象**，对一个操作也会影响另一个，需要去仅仅把值拷贝一份给新的对象，再添加到数组中：

```
//错误
addedTags.push（originTags[idx]）;

//正确
let tagToAdd = Object.assign({},originTags[idx])
tagToAdd.attr1 = true;
addedTags.push(tagToAdd);
```

### （4）判断对象是否为空对象（用JSON.stringfy() 判断是否 等于 '{}'）



```
const a = {};
JSON.stringify(a) == '{}' //true
```





## 二 常用方法

### 1. 对象属性的遍历 for in 循环


例子

```
var person={fname:"Bill",lname:"Gates",age:56};

for (let x in person)
  {
  txt=txt + person[x];  // 参数x代表属性名
  }
```

详细参考
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in

### Object.keys() 返回对象的自身可枚举属性组成的数组


###  delete 操作符  用于删除对象的某个属性。

语法
delete expression
 expression 的计算机结果应该是某个属性的引用，例如：

delete object.property 
delete object['property']



例子


```
var Employee = {
  age: 28,
  name: 'abc',
  designation: 'developer'
}

console.log(delete Employee.name);   // returns true
console.log(delete Employee.age);    // returns true

// 当试着删除一个不存在的属性时
// 同样会返回true
console.log(delete Employee.salary); // returns true
```



https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete
































