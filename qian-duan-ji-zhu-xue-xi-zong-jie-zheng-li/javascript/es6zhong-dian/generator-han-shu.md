# Generator 函数

## 一 简介
ES6 提供的一种异步编程解决方案

### 作用
可以理解成，**Generator 函数是一个状态机，封装了多个内部状态**。

**执行 Generator 函数会返回一个遍历器对象**，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，**可以依次遍历 Generator 函数内部的每一个状态**。


## 二 语法与使用

### 1. Generator 函数基本结构

形式上，Generator 函数是普通函数，但有两个特征：

1. function关键字与函数名之间有一个星号 * 

2. 函数体内部使用yield表达式，定义不同的内部状态（yield在意为“产出”）

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

### 2. Generator 函数的调用

调用方法也是在函数名后加圆括号。
不同的是，**调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象（即遍历器对象）**。



## 三 Generator 函数的异步应用


## 参考
ECMAScript 6 入门 - Generator 函数的语法
http://es6.ruanyifeng.com/#docs/generator

ECMAScript 6 入门 - Generator 函数的异步应用
http://es6.ruanyifeng.com/#docs/generator-async



