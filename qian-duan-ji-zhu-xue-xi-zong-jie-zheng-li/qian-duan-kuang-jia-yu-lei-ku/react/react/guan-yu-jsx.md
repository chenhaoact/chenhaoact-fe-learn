### 2 关于jsx

#### （1）jsx概念

JavaScript 中 XML 式的语法。有一个简单的预编译器，将该语法糖转换成这种纯的JavaScript。

JSX 语法比单纯的 JavaScript 更加容易使用（特别是编写渲染html元素相关的代码时）。阅读更多关于[JSX 语法的文章](http://www.react-cn.com/docs/jsx-in-depth-zh-CN.html)。

jsx**可以在类似html的标签中通过{}里面写js变量与表达式。**

JSX可以混合 HTML 标签和自己建立的组件：

在**JSX中写的HTML 标签也会作为正常的 React 组件**，就和你定义的一样，只有一个区别。

**JSX 编译器会自动重写 HTML 标签为 React.createElement\(tagName\) 表达式，其它什么都不做**。这是为了**避免污染全局命名空间**。

#### （2）jsx的设计理念

react的设计者坚信关注分离的正确方法是组件，而非通过“模板”和“展示逻辑”。他们认为**标签和生成它的代码是紧密相连的**。此外，**展示逻辑通常很复杂，通过模板语言实现会产生大量代码。**

设计者们得出**解决这个问题最好的方案是通过 JS 直接生成模板**，这样你就可以用一个真正语言的所有表达能力去构建用户界面。

为了使这变得更简单，设计者就做了一个非常简单、可选类似 HTML 语法 ，通过函数调用即可生成模板的编译器，称为 JSX。

**JSX让你可以把JavaScript函数调用和HTML语法写在一起。**

#### （3）HTML转义
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


React默认会进行HTML的转义，避免XSS攻击，如果要不转义，可以这么写



```
var content='<strong>content</strong>';    

React.render(
    <div dangerouslySetInnerHTML={{__html: content}}></div>,
    document.body
);
```
