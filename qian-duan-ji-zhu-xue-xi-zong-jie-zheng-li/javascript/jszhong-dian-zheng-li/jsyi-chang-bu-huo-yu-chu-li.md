# js异常捕获与处理

## 一 Error对象
Js解析或执行时，一旦发生错误，引擎就会抛出一个错误对象。Js原生提供Error构造函数，所有抛出的错误都是这个构造函数的实例。

```
var err = new Error('出错了');
```

**代码解析或运行时发生错误，Js引擎会自动产生、并抛出一个Error对象实例，整个程序就中断在发生错误的地方，不再往下执行**。

Error对象的实例必须有**message属性，表示出错时的提示信息**。大多数Js引擎，对Error实例还提供name和stack属性，分别表示错误的名称和错误的堆栈。

## 二 Js的原生错误类型
Error对象是最一般的错误类型，在它的基础上，Js定义了其他6种错误(Error的6个派生对象)

###（1）SyntaxError
解析代码时发生的语法错误。

###（2）ReferenceError
引用一个不存在的变量时发生的错误。
另一种触发场景是，将一个值分配给无法分配的对象，比如对函数的运行结果或者this赋值。

### （3）RangeError
当一个值超出有效范围时发生的错误。主要有几种情况，一是数组长度为负数，二是Number对象的方法参数超出范围，以及函数堆栈超过最大值。

### （4）TypeError
TypeError是变量或参数不是预期类型时发生的错误。比如，对字符串、布尔值、数值等原始类型的值使用new命令，就会抛出这种错误，因为new命令的参数应该是一个构造函数。

###（5）URIError
URIError是URI相关函数的参数不正确时抛出的错误，主要涉及encodeURI()、decodeURI()、encodeURIComponent()、decodeURIComponent()、escape()和unescape()这六个函数。

###（6）EvalError

eval函数没有被正确执行时，会抛出EvalError错误。该错误类型已经不再在ES5中出现了，为保证与以前代码兼容，才保留的。

### 使用
**以上6种派生错误，连同原始的Error对象，都是构造函数。开发者可以使用它们，人为生成错误对象的实例。**


```
new Error('出错了！');
new RangeError('出错了，变量超出有效范围！');
new TypeError('出错了，变量类型无效！');
```

上面代码新建错误对象的实例，实质就是手动抛出错误。错误对象的构造函数接受一个参数，代表错误提示信息（message）。

### 三 自定义错误

自定义一个错误对象UserError，让它继承Error对象。然后，就可以生成这种自定义的错误了。

### 四 throw语句

**throw语句的作用是中断程序执行，抛出一个意外或错误。**

它接受一个表达式作为参数，可以抛出各种值（字符串，数字，对象等）。

**throw可以接受各种值作为参数。Js引擎一旦遇到throw语句，就会停止执行后面的语句，并将throw语句的参数值，返回给用户。**

如果只是简单错误，返回一条出错信息就可以，但如果**遇到复杂情况，就需要在出错后进一步处理。这时最好的做法是使用throw语句手动抛出一个Error对象:**


```
throw new Error('出错了!');
```

上面语句新建一个Error对象，将这个对象抛出，整个程序就中断在这里。

throw语句还可以抛出用户自定义的错误。

### 五 try…catch语句
为了**对错误进行处理，需要使用try...catch结构**。

```
try {
  throw new Error('出错了!');
} catch (e) {
  console.log(e.name + ": " + e.message);
  console.log(e.stack);
}
// Error: 出错了!
//   at <anonymous>:3:9
//   ...

```

**try代码块一抛出错误**（上例用的是throw语句），**Js引擎就立即把代码的执行，转到catch代码块**。可以看作，**错误可以被catch代码块捕获。catch接受一个参数为try代码块抛出的值**。

**catch代码块捕获错误之后，程序不会中断，会按照正常流程继续执行下去。**

注意：
try...catch结构是Js受到Java语言影响的一个明显的例子。虽然可以捕获到错误并保证程序的正常运行，但这种结构多多少少是对结构化编程原则一种破坏，处理不当会变成类似goto语句的效果，使用时要谨慎一些。

### 六 finally代码块
try...catch结构允许在最后添加一个**finally代码块，表示不管是否出现错误，都必需在最后运行的语句**。

下面是**finally代码块用法的典型场景：**

```
openFile();

try {
  writeFile(Data);
} catch(e) {
  handleError(e);
} finally {
  closeFile();
}

```

上面代码首先打开一个文件，然后在try代码块中写入文件，如果没有发生错误，则运行finally代码块关闭文件；一旦发生错误，则先使用catch代码块处理错误，再使用finally代码块关闭文件。

下面的例子反映**try...catch...finally三者间的执行顺序：**

```
function f() {
  try {
    console.log(0);
    throw 'bug';
  } catch(e) {
    console.log(1);
    return true; // 这句原本会延迟到finally代码块结束再执行
    console.log(2); // 不会运行
  } finally {
    console.log(3);
    return false; // 这句会覆盖掉前面那句return
    console.log(4); // 不会运行
  }

  console.log(5); // 不会运行
}

var result = f();
// 0
// 1
// 3

result
// false

```

上面代码中，**catch代码块结束执行前（注意是结束执行之前），会先执行finally代码块。从catch转入finally的标志，不仅有return语句，还有throw语句。**



## 参考
## 已学习
[《JavaScript 标准参考教程（alpha）》，by 阮一峰 语法-错误处理机制](http://javascript.ruanyifeng.com/grammar/error.html)

## 待学习