### 2 关于jsx

#### （1）jsx概念

JavaScript 中 XML 式的语法。有一个简单的预编译器，将该语法糖转换成这种纯的JavaScript。

**JSX 语法比单纯的 JS 更加容易使用（特别是编写渲染html元素相关的代码时）**。阅读更多关于[JSX 语法的文章](http://www.react-cn.com/docs/jsx-in-depth-zh-CN.html)。

jsx**可以在类似html的标签中通过{}里面写js变量与表达式。**

JSX可以混合 HTML 标签和自己建立的组件：

在**JSX中写的HTML 标签也会作为正常的 React 组件**，就和你定义的一样，只有一个区别。

**JSX 编译器会自动重写 HTML 标签为 React.createElement\(tagName\) 表达式，其它什么都不做**。这是为了**避免污染全局命名空间**。

#### （2）jsx的设计理念

react的设计者坚信关注分离的正确方法是组件，而非通过“模板”和“展示逻辑”。他们认为**标签和生成它的代码是紧密相连的**。此外，**展示逻辑通常很复杂，通过模板语言实现会产生大量代码。**

设计者们得出**解决这个问题最好的方案是通过 JS 直接生成模板**，这样你就可以用一个真正语言的所有表达能力去构建用户界面。

为了使这变得更简单，设计者就做了一个非常简单、可选类似 HTML 语法 ，通过函数调用即可生成模板的编译器，称为 JSX。

**JSX让你可以把JavaScript函数调用和HTML语法写在一起。**

#### （2）jsx语法注意点

属性名一律使用驼峰法，而不是一般html元素的属性写法。

属性值要么用""引用字符串，要么是{}里嵌套js表达式,两者不能混。

元素为空，需要以 `/>`关闭。


#### （4）HTML转义
比如我们有一些内容是用户输入的富文本，从后台取到数据后展示在页面上，希望展示相应的样式



```
var content='<strong>content</strong>';

React.render(
    <div>{content}</div>,
    document.body
);
```


结果页面直接输出内容了



```
<stonrg>content</strong>
```


**React的jsx默认会进行HTML的转义（将变量转为其值的字符串来展现），避免XSS攻击**，如果**要不转义，可以用dangerouslySetInnerHTML属性(数据设置为到__html的值)**这么写：



```
var content='<strong>content</strong>';    

React.render(
    <div dangerouslySetInnerHTML={{ __html: content }}></div>,
    document.body
);
```

具体可参考此文html转义部分：http://yijiebuyi.com/blog/2e3b6f3a01983e46c3aaca4f28377a28.html

#### （5）jsx也是一种表达式，在编译之后会成为js对象

**jsx也是一种表达式，在编译之后会成为js对象。**
这意味着**可以在if,for等各种js语句中使用jsx，把他们和变量写在一起，或者作为参数接收，或者从js函数中返回**:


```

function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}

```

##### jsx代表对象

**Babel 编译 JSX 调用的是 React.createElement().**
以下两个例子，完全相同：



```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```



```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);

```


**React.createElement() 会执行一些代码检查，并扩展性的创建类似以下的一个对象**:

```
// 注意: 这里是经过简化的结构
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```

这样的对象称为 "**React elements**". 可以把它们当做是**对屏幕中显示的元素的描述**。 React 会**读取这些对象并通过他们构建DOM和保持DOM显示的数据能实时更新**。









