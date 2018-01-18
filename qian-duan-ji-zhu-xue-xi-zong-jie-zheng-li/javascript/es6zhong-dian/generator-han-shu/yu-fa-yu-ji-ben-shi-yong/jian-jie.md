## 一 简介
**Generator 函数**是 ES6 提供的一种异步编程解决方案。
**Generator 能生成了一系列的值，这也就是它的名称的来历（英语中，generator 是“生成器”**的意思）。

### 1. Generator 函数的 本质与用途
可以理解成，**Generator 函数是一个状态机，封装了多个内部状态**。

**执行 Generator 函数会返回一个遍历器对象**，也就是说，Generator 函数除了状态机，**它还是一个遍历器对象生成函数**。返回的遍历器对象，**可依次遍历 Generator 函数内的每个状态**。


### 2. Generator 函数基本结构

形式上，Generator 函数是普通函数，但有两特征：

1. **function关键字与函数名之间有一个星号 * **

2. **函数体内部使用yield表达式，定义不同的内部状态（yield意为“产出”）**

例子


```
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```
该函数有三状态：hello，world 和 return 语句（结束执行）。

ES6 没有规定，function关键字与函数名之间的星号，写在哪个位置。**一般推荐的写法*号紧跟在function关键字后面**。

```
function* foo(x, y) { ··· }
```

### 3. Generator 函数的调用

**调用方法也是在函数名后加圆括号**。

**不同的是，调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象（即遍历器对象）**。



```
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```


**加圆括号调用获取到遍历器对象后，下一步，必须调用遍历器对象的next方法，使得指针移向下一个状态**。也就是说，每次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，**直到遇到下一个yield表达式（或return语句）为止**。换言之，Generator 函数是分段执行的，yield表达式是暂停执行的标记，而next方法可恢复执行。



```
hw.next()
// { value: 'hello', done: false }

hw.next()
// { value: 'world', done: false }

hw.next()
// { value: 'ending', done: true }

hw.next()
// { value: undefined, done: true }
```

总结下，调用 Generator 函数，返回一个遍历器对象，代表 Generator 函数的内部指针。以后，**每次调用遍历器对象的next方法，就会返回一个有着value和done两个属性的对象**。
**value属性表示当前的内部状态的值，是yield表达式后面那个表达式的值；done属性是一个布尔值，表示是否遍历结束**。


### 5. yield 表达式

yield表达式是暂停标志。

遍历器对象的next方法的运行逻辑如下。

（1）遇到yield表达式，就暂停执行后面的操作，**并将紧跟在yield后面的那个表达式进行求值，作为返回的对象的value**属性值。

（2）下一次调用next方法时，再继续往下执行，直到遇到下一个yield表达式。

（3）如果没再遇到新yield表达式，就一直运行到函数结束，直到return语句为止，并将return语句后面的表达式的值，作为返回的对象的value属性值。

（4）如果**该函数没有return语句，则返回的对象的value属性值为undefined**。

**yield表达式后面的表达式**，只有当调用next方法、**内部指针指向该语句时才会执行求值**。

#### yield和return的区别
return语句不具备位置记忆的功能。一个函数里面，只能执行一次return语句，但可以执行多个yield表达式

#### 普通函数中使用yield表达式会报错，故循环不能用forEach可以用for循环

```

var arr = [1, [[2, 3], 4], [5, 6]];

var flat = function* (a) {
  a.forEach(function (item) {
    if (typeof item !== 'number') {
      yield* flat(item);
    } else {
      yield item;
    }
  });
};

for (var f of flat(arr)){
  console.log(f);
}
```

上面代码会产生句法错误，因为forEach方法的参数是一个普通函数，但里面使用了yield表达式。一种**修改方法是改用for循环**。

#### yield表达式如果用在另一个表达式之中，必须放在圆括号里面。


### Generator 函数可以不用yield表达式，变成一个暂缓执行函数

```
function* f() {
  console.log('执行了！')
}

var generator = f();

setTimeout(function () {
  generator.next()
}, 2000);
```



上面代码，**函数f如果是普通函数，在为变量generator赋值时（因为f后加了（））就会执行**。但函数f是一个 Generator 函数，就**变成只有调用next方法时，函数f才会执行**。



### 6. 与 Iterator 接口的关系










