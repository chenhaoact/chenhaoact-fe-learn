## yield* 表达式
### yield*表达式，用来在一个 Generator 函数里面执行另一个 Generator 函数。

因为一般的形式在 Generator 函数内部，调用另一个 Generator 函数，默认情况下是没有效果的。如：



```
function* foo() {
  yield 'a';
  yield 'b';
}

function* bar() {
  yield 'x';
  foo();
  yield 'y';
}

for (let v of bar()){
  console.log(v);
}
// "x"
// "y"
```

要使用yield*表达式才行：



```
function* bar() {
  yield 'x';
  yield* foo();
  yield 'y';
}

// 等同于
function* bar() {
  yield 'x';
  yield 'a';
  yield 'b';
  yield 'y';
}

// "x"
// "a"
// "b"
// "y"
```



### yield*后面的 Generator 函数（没有return语句时），等同于在 Generator 函数内部，部署一个for...of循环



