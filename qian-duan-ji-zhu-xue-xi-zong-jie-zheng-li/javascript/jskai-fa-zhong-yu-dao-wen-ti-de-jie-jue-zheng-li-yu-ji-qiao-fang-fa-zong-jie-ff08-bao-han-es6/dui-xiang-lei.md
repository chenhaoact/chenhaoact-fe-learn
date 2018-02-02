## 对象类

### 1. 读取对象的属性 必须要保证对象已定义且非空，否则会抛异常导致页面白屏等


```
a = null  //或者 a = undefined
a.bbb   //  js抛异常  cannot read property ...

a = {}
a.bbb  // undefined
```

所有读任务对象的属性值时必须保证该对象是存在的，

**一般声明变量的时候，就给一个初始值，是一个避免此类异常的好方法**：



```
let a = {}, b = '', c = [];  // 不要写let a,b,c;  很容易因为初始值为undefined而出问题！   

```



### 2. 对象（包括数组等本质是对象的数据结构）赋值不要用 = ，用 = 相当于是给了引用，最后修改的时候还会修改原对象，造成污染，可以用 es6的 Object.assign() 去赋值对象值到新的对象里：

```
//let itemToChange = item; item是对象时，错，改变itemToChange时会改动原来的item

let itemToChange = Object.assign({},item);
itemToChange.a = 'a';
```







