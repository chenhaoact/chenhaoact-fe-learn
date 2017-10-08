## 虚拟dom（重点）

React开发时是不会去操作DOM的。它用一种更快的内置的**虚拟 DOM 来操作差异**，计算出效率最高的 DOM 改变。

**React非常快速是因为它从不直接操作DOM**。React维持了一个快速的内存中的DOM表示。render\(\) 方法实际上返回一个对DOM的描述，然后React能将其与内存中的“描述”进行比较，以计算出最快速的方式更新浏览器。

### 虚拟dom原理

#### （1）从源码看react组件的渲染流程：

ReactDOM.render(）是渲染React组件并插入到DOM中的入口方法，它的执行流程大概为：

1. React.createElement(),创建ReactElement对象。他的重要的成员变量有type,key,ref,props。这个过程中会调用getInitialState(), 初始化state，只在挂载的时候才调用。后面update时不再调用了。

2. instantiateReactComponent()，根据ReactElement的type分别创建ReactDOMComponent， ReactCompositeComponent，ReactDOMTextComponent等对象

3. mountComponent(), 调用React生命周期方法解析组件，得到它的HTML。

4. _mountImageIntoNode(), 将HTML插入到DOM父节点中，通过设置DOM父节点的innerHTML属性。

5. 缓存节点在React中的对应对象，即Virtual DOM。

#### diff算法

** TODO??? 
** 
 参考：
 深入浅出React（四）：虚拟DOM Diff算法解析
 http://www.infoq.com/cn/articles/react-dom-diff
 
 React 的 diff 算法
 https://segmentfault.com/a/1190000000606216
 
 React源码剖析系列 － 不可思议的react diff
https://zhuanlan.zhihu.com/purerender/20346379

## 访问dom\(通过Refs 和 findDOMNode\(\)\)

React提供了强大的抽象机制使大多数情况下免于直接接触DOM，但**有时你仅仅只需要访问底层API，或许是为了与第三方库比如一个jQuery插件协作。React为你提供了安全入口来直接使用底层API**。

为了与浏览器互动，需要一个指向DOM node的引用。可以连接一个 ref 到任何的元素，这允许你引用组件的 backing instance 。如果你需要在组件上调用命令式函数，或者想访问底层的DOM节点，它很有用。

Refs的具体使用参考：  
[https://facebook.github.io/react/docs/refs-and-the-dom.html](https://facebook.github.io/react/docs/refs-and-the-dom.html)

