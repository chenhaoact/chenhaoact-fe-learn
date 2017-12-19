# ES6 Array 新特性

#### （1）使用扩展运算符（...）拷贝数组

```
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

#### （2）使用 Array.from 方法，将类似数组的对象转为数组



```
const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```





