### 虚拟dom

React开发时是不会去操作DOM的。它用一种更快的内置的**虚拟 DOM 来操作差异**，计算出效率最高的 DOM 改变。

**React非常快速是因为它从不直接操作DOM**。React维持了一个快速的内存中的DOM表示。render\(\) 方法实际上返回一个对DOM的描述，然后React能将其与内存中的“描述”进行比较，以计算出最快速的方式更新浏览器。

#### 访问dom\(通过Refs 和 findDOMNode\(\)\)

React提供了强大的抽象机制使大多数情况下免于直接接触DOM，但**有时你仅仅只需要访问底层API，或许是为了与第三方库比如一个jQuery插件协作。React为你提供了安全入口来直接使用底层API**。

为了与浏览器互动，需要一个指向DOM node的引用。可以连接一个 ref 到任何的元素，这允许你引用组件的 backing instance 。如果你需要在组件上调用命令式函数，或者想访问底层的DOM节点，它很有用。

Refs的具体使用参考：  
[https://facebook.github.io/react/docs/refs-and-the-dom.html](https://facebook.github.io/react/docs/refs-and-the-dom.html)

