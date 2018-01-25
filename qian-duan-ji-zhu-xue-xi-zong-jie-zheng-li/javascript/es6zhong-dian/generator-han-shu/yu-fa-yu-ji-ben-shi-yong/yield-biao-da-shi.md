# next 方法的参数

yield表达式本身没返回值(返回undefined)。
### next方法可以带一个参数，该参数会被当作上一个yield表达式的返回值。**



```
function* f() {
  for(var i = 0; true; i++) {
    var reset = yield i;
    if(reset) { i = -1; }
  }
}

var g = f();

g.next() // { value: 0, done: false }
g.next() // { value: 1, done: false }
g.next(true) // { value: 0, done: false }
```

**这个功能很重要。**Generator 函数从暂停状态到恢复运行，它的上下文状态（context）是不变的。**通过next方法的参数，能在 Generator 函数开始运行后，继续向函数体内注入值。**

即：**可在 Generator 函数运行的不同阶段，从外部向内部注入不同的值，从而调整函数行为**。

### 由于next方法的参数表示上一个yield表达式的返回值，在第一次使用next方法时，传递参数无效

V8 引擎直接忽略第一次next方法时的参数，只有从第二次使用next方法开始，参数才是有效的。从语义上讲，第一个next方法用来启动遍历器对象，不用带有参数。






