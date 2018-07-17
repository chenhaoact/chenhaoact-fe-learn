# Iterator 和 for...of 循环及js各种遍历的比较

## Iterator
遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

Iterator 的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令for...of循环，Iterator 接口主要供for...of消费。

Iterator 的遍历过程是这样的。

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的next方法，直到它指向数据结构的结束位置。

每一次调用next方法，都会返回数据结构的当前成员的信息。具体来说，就是返回一个包含value和done两个属性的对象。其中，value属性是当前成员的值，done属性是一个布尔值，表示遍历是否结束。

## for...of 循环
### for...of 循环和Symbol.iterator属性的关系
Iterator 接口的目的，就是为所有数据结构，提供了一种统一的访问机制，即for...of循环。

一个数据结构只要部署了Symbol.iterator属性，就被视为具有 iterator 接口，就可用for...of循环遍历它的成员。for...of循环内部调用的是数据结构的Symbol.iterator方法。

### for...of循环可以使用的范围包括：
数组、Set 和 Map 结构、某些类似数组的对象（比如arguments对象、DOM NodeList 对象）、后文的 Generator 对象，以及字符串。

### for...of循环的使用（重点）
for...of循环可以代替数组实例的forEach方法。

Js 原有的**for...in**循环，**只能获得对象的键名**，不能直接获取键值。ES6 提供**for...of循环，允许遍历获得键值**。


```
var arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a); // 0 1 2 3
}

for (let a of arr) {
  console.log(a); // a b c d
}
```

## 各种js遍历语法的比较（重点！）
以数组为例，JavaScript 提供多种遍历语法。最原始的写法就是**（1）for循环**：



```
for (var index = 0; index < myArray.length; index++) {
  console.log(myArray[index]);
}
```


这种写法比较麻烦，因此数组提供内置的**（2）forEach方法**。


```
myArray.forEach(function (value) {
  console.log(value);
});

```


**forEach写法的问题在于，无法中途跳出forEach循环，break命令或return命令都不能奏效**。

**（3）for...in循环可以遍历数组的键名**。

```
for (var index in myArray) {
  console.log(myArray[index]);
}
```

for...in循环有几个缺点

数组的键名是数字，但是for...in循环是以字符串作为键名“0”、“1”、“2”等。
for...in循环不仅遍历数字键名，还会遍历手动添加的其他键，甚至包括原型链上的键。
某些情况，for...in循环会以任意顺序遍历键名。

总之，**for...in循环主要是为遍历对象而设计的，不适用于遍历数组**。


**（4）for...of循环相比上面几种做法，有一些显著的优点：**

```
for (let value of myArray) {
  console.log(value);
}
```

有着同for...in一样的简洁语法，但是没有for...in那些缺点。
不同于forEach方法，它**可以与break、continue和return配合使用**。
提供了遍历所有数据结构的统一操作接口。


**所以，循环遍历，建议统一优先使用for...of 。**







