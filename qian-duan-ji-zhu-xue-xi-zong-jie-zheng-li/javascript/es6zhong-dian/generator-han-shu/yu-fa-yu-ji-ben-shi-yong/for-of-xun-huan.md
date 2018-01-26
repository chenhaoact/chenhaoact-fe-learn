# for...of 循环
###1. for...of循环可自动遍历 Generator 函数生成的Iterator对象，且此时不再需要调用next方法。



```
function* foo() {
  yield 1;
  yield 2;
  yield 3;
  yield 4;
  yield 5;
  return 6;
}

for (let v of foo()) {
  console.log(v);
}
// 1 2 3 4 5
```


上面代码用for...of循环，依次显示 5 个yield表达式的值。

###2. **一旦next方法返回对象的done属性为true，for...of循环就中止，且不包含该返回对象，所以代码的return语句的返回值（6），不在for...of循环中**

###3. 利用for...of循环，可写出遍历任意对象（object 的key  value）的方法

原生JS 对象没遍历接口，无法用for...of循环，通过 Generator 函数为它加上这个接口，就可以用了。



```
function* objectEntries(obj) {
  let propKeys = Reflect.ownKeys(obj);

  for (let propKey of propKeys) {
    yield [propKey, obj[propKey]];
  }
}

let jane = { first: 'Jane', last: 'Doe' };

for (let [key, value] of objectEntries(jane)) {
  console.log(`${key}: ${value}`);
}
// first: Jane
// last: Doe
```



上面代码中，对象jane原生不具备 Iterator 接口，无法用for...of遍历。**通过 Generator 函数objectEntries为它加上遍历器接口，就可以用for...of遍历了**。

**加上遍历器接口的另一种写法是，将 Generator 函数加到对象的Symbol.iterator属性上**。



```
function* objectEntries() {
  let propKeys = Object.keys(this);

  for (let propKey of propKeys) {
    yield [propKey, this[propKey]];
  }
}

let jane = { first: 'Jane', last: 'Doe' };

jane[Symbol.iterator] = objectEntries;

for (let [key, value] of jane) {
  console.log(`${key}: ${value}`);
}
// first: Jane
// last: Doe
```

###4. 除了for...of循环外，扩展运算符（...）、解构赋值和Array.from方法内调用的，都是遍历器接口。它们都可将 Generator 函数返回的 Iterator 对象，作为参数。



```
function* numbers () {
  yield 1
  yield 2
  return 3
  yield 4
}

// 扩展运算符
[...numbers()] // [1, 2]

// Array.from 方法
Array.from(numbers()) // [1, 2]

// 解构赋值
let [x, y] = numbers();
x // 1
y // 2

// for...of 循环
for (let n of numbers()) {
  console.log(n)
}
// 1
// 2
```





