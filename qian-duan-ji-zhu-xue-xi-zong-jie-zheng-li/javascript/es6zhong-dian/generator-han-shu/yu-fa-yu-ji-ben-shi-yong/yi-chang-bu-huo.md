# 异常捕获

## 1. Generator的throw() 方法

**Generator 函数返回的遍历器对象，都有throw方法，可在函数体外抛出错误，然后在 Generator 函数体内捕获**。



```
var g = function* () {
  try {
    yield;
  } catch (e) {
    console.log('内部捕获', e);
  }
};

var i = g();
i.next();

try {
  i.throw('a');
  i.throw('b');
} catch (e) {
  console.log('外部捕获', e);
}
// 内部捕获 a
// 外部捕获 b
```


上面代码，遍历器对象i连续抛出两个错误。**第一个错误被 Generator 函数体内的catch语句捕获**。i**第二次抛出错误**，由于 Generator 函数内部的catch语句已经执行过了，不会再捕捉到这个错误了，所以这个错误就被抛出了 Generator 函数体，**被函数体外的catch语句捕获**。

## 2. throw方法接受的参数
throw方法可以接受一个参数，该参数会被catch语句接收，**建议抛出Error对象的实例**。



```
var g = function* () {
  try {
    yield;
  } catch (e) {
    console.log(e);
  }
};

var i = g();
i.next();
i.throw(new Error('出错了！'));
// Error: 出错了！(…)

```

注意，**不要混淆遍历器对象的throw方法和全局的throw命令**。上面代码的错误，是用遍历器对象的throw方法抛出的，而不是用**全局的throw命令（只能被函数体外的catch语句捕获）**抛出的。

## 3. 如 Generator 函数内没部署try...catch代码块，那throw方法抛出的错误，将被外部try...catch代码块捕获

## 4. 特别注意！！！如Generator 函数内部外部，都没部署try...catch代码块，那么程序报错则直接中断执行。



```
var gen = function* gen(){
  yield console.log('hello');
  yield console.log('world');
}

var g = gen();
g.next();
g.throw();
// hello
// Uncaught undefined
```


上面代码，g.throw抛出错误后，没有任何try...catch代码块可以捕获，导致程序报错，中断执行。

## 5. throw方法被捕获以后，会附带执行下一条yield表达式。也就是说，会附带执行一次next方法

只要 Generator 函数内部部署了try...catch代码块，那么遍历器的throw方法抛出的错误，不影响下一次遍历。

## 6. 这种函数体内捕获错误的机制，大大方便了对错误的处理。多个yield表达式，可以只用一个try...catch代码块来捕获错误。
如果使用回调函数的写法，想要捕获多个错误，就不得不为每个函数内部写一个错误处理语句，现在只在 Generator 函数内部写一次catch语句就可以了。


## 7. Generator 函数体外抛出的错误，可以在函数体内捕获；反过来，Generator 函数体内抛出的错误，也可以被函数体外的catch捕获。



```
function* foo() {
  var x = yield 3;
  var y = x.toUpperCase();
  yield y;
}

var it = foo();

it.next(); // { value:3, done:false }

try {
  it.next(42);
} catch (err) {
  console.log(err);
}
```


上面代码中，第二个next方法向函数体内传入一个参数 42，数值是没有toUpperCase方法的，所以会抛出一个 TypeError 错误，被函数体外的catch捕获。

## 8. 一旦 Generator 执行过程中抛出错误，且没有被内部捕获，就不会再执行下去了。如果此后还调用next方法，将返回一个value属性等于undefined、done属性等于true的对象，即 JS 引擎认为这个 Generator 已经运行结束了。


```
function* g() {
  yield 1;
  console.log('throwing an exception');
  throw new Error('generator broke!');
  yield 2;
  yield 3;
}

function log(generator) {
  var v;
  console.log('starting generator');
  try {
    v = generator.next();
    console.log('第一次运行next方法', v);
  } catch (err) {
    console.log('捕捉错误', v);
  }
  try {
    v = generator.next();
    console.log('第二次运行next方法', v);
  } catch (err) {
    console.log('捕捉错误', v);
  }
  try {
    v = generator.next();
    console.log('第三次运行next方法', v);
  } catch (err) {
    console.log('捕捉错误', v);
  }
  console.log('caller done');
}

log(g());
// starting generator
// 第一次运行next方法 { value: 1, done: false }
// throwing an exception
// 捕捉错误 { value: 1, done: false }
// 第三次运行next方法 { value: undefined, done: true }
// caller done

```

上面代码一共三次运行next方法，第二次运行时会抛出错误，第三次运行时，Generator 函数已结束，不再执行下去了。






