## 对象类

### 对象（包括数组等本质是对象的数据结构）赋值不要用 = ，用 = 相当于是给了引用，最后修改的时候还会修改原对象，造成污染，可以用 es6的 Object.assign() 去赋值对象值到新的对象里：

```
//let itemToChange = item; item是对象时，错，改变itemToChange时会改动原来的item

let itemToChange = Object.assign({},item);
itemToChange.a = 'a';
```







