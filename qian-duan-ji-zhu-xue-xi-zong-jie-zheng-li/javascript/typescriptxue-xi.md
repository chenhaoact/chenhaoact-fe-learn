# typescript总结

## 一 简介

### 1用途

JavaScript的超集，可编译成纯JavaScript。

### 2优缺点及对比

可以编译出纯净、 简洁的JavaScript代码，并且可以运行在任何浏览器上、Node.js环境中和任何支持ECMAScript 3（或更高版本）的JavaScript引擎中。

**通过类型注解提供编译时的静态类型检查。（在数据类型上相比js可以更严格一些）**

类型允许JavaScript开发者在开发JavaScript应用程序时使用高效的开发工具和常用操作比如静态检查和代码重构。

提供最新的和不断发展的JavaScript特性，包括那些来自ES6和未来的提案中的特性。这些特性为高可信应用程序开发时是可用的，但是会被编译成简洁的ECMAScript3（或更新版本）的JavaScript。

angular2开始采用了typescript，所以目前受到微软和谷歌两大公司的支持。

## 二 基本概念与技术重点整理

### 1基本数据类型新特性

#### （1）模板字符串：

可以定义**多行文本**和**内嵌表达式**。 这种字符串是被反引号包围（`````````），并且以`````${ expr }\`嵌入表达式（可带变量和函数）

如：

    let name: string = `Gene`;
    let age: number = 37;
    let sentence: string = `Hello, my name is ${ name }.

    I'll be ${ age + 1 } years old next month.`;

与下面定义相同：

```
let sentence: string = "Hello, my name is " + name + ".\n\n" +
    "I'll be " + (age + 1) + " years old next month.";
```

#### （2）自动拆分字符串

用字符串模板去调用函数时，字符串模板里表达式的值，会自动赋值给函数中的参数。

    function test(template, name, gender) {
        console.log(template);
        console.log(name)
        console.log(gender)
    }
    var myName = "tang quan kun";
    var getGender = function(){
        return "男";
    }
    test`my name is ${myName},my gender is ${getGender()}`

![](/assets/string4.png)

从打印的结果可以看,其中第一个打印的是一个字符串的数组，第二打印的是tang quan kun 第三个打印的是 男，第一个参数template接收是传入的字符串，第二个为拆分的表达式`${myName}`，第三个为拆分的表达式`${getGender}`

#### （3）元组 Tuple

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，可定义一对值分别为 string和number类型的元组。

```
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error
```

#### （4）枚举（enum）

enum类型是对JavaScript标准数据类型的一个补充。 像C\#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

#### （5）指定参数类型（重要！）

**参数后面使用冒号来指定参数的类型**

```
let myName: string = "chenhaoact"
    myName = 12 //error，要能变类型，上面可以声明类型为any
```

#### （6）任意类型（any）

```
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

对现有代码进行改写的时候，any类型是十分有用的，它允许你在编译时可选择地包含或移除类型检查。

#### \(7\)空值类型\(void\)

某种程度上来说，void类型像是与any类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 void

```
function warnUser(): void {
    alert("This is my warning message");
}
```

#### （8）类型断言

类型断言有两种形式。 其一是“尖括号”语法

```
let strLength: number = (<string>someValue).length;
```

另一个为as语法：

```
let strLength: number = (someValue as string).length;
```

在TypeScript里使用JSX时，只有as语法断言是被允许。

### 2函数新特性

#### （1）给函数参数设置默认值 （=）

在参数声明后面用=来指定参数的默认值。

```
function test(a: string, b: string, c: string = "zzz") {
    console.log(a)
    console.log(b)
    console.log(c)
}
test("xxx","yyy")
```

会打印出xxx,yyy,zzz。

注意：只能够把指定默认值得参数方式最后面，如果不放在最后面会报错误。

#### （2）可选参数 （？）

在方法的后面用**问号**来标明此参数为可选参数。

```
function test(a: string, b?: string, c: string = "zzz") {
    console.log(a)
    console.log(b)
    console.log(c)
}
test("yyy")
```

会打印出xxx,undefined,zzz,因为b元素为可选元素，所以用test\(“yyy”\)调用不会报错，c有默认值

### 3面向对象特性

### 

## 三 使用实践及案例

### 1安装编译器

安装命令行的TypeScript编译器（可以通过命令对ts代码进行编译如：转化为es5的代码等）：

`npm install -g typescript`

比如创建一个ts编写的文件helloworld.ts，运行以下命令:

`tsc helloworld.ts`

就能在同目录下生成等效的js代码文件helloworld.js

### 2使用webstorm的ts编译器支持

创建一个项目（这里我创建在本地的/project/front/BasicLearn下的TypeScriptLearn）。

创建01-basic-types.ts，在右侧会出现：![](/assets/importtstst.png)

点Configure，勾选Enable Typescript Compiler，点Apply后点OK：

![](/assets/importgg.png)

这时，webstorm就会去自动的执行tsc命令，在ts文件的同目录下实时的生成js文件：

![](/assets/importssssssjs.png)![](/assets/importssssjsjsjs.png)

## 四 资源

### 1官网

英文官网

[https://www.typescriptlang.org/](https://www.typescriptlang.org/)

中文官网**（中文网上的ts版本会落后于英文官网，所以学习最新的typescript最好以英文官网为主）**

[https://www.tslang.cn/](https://www.tslang.cn/)

### 2文档

英文最新文档

[https://www.typescriptlang.org/docs/home.html](https://www.typescriptlang.org/docs/home.html)

中文文档

[https://www.tslang.cn/docs/tutorial.html](https://www.tslang.cn/docs/tutorial.html)

### 3源码

[https://github.com/Microsoft/TypeScript](https://github.com/Microsoft/TypeScript)

### 4教程

官方教程：

[https://www.typescriptlang.org/samples/index.html](https://www.typescriptlang.org/samples/index.html)

其他教程：
TypeScript 入门教程
http://www.runoob.com/w3cnote/getting-started-with-typescript.html

慕课网TypeScript入门视频教程

[http://www.imooc.com/learn/763](/h ttp://www.imooc.com/learn/763)

该视频课程代码与博客参考：

https://wxxtqk.github.io/2017/02/09/typescript01/



### 5工具与资源

在线编译（将ts的代码转为js代码（es5））

[https://www.typescriptlang.org/play/index.html](https://www.typescriptlang.org/play/index.html)

