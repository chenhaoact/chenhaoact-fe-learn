有了它还并不能直接在浏览器中渲染，因为还需要一个 render 过程，就是我们在React中写的 render() 方法，render方法的定义在src/renderers/dom/stack/client/ReactMount.js:

![](/assets/WX20171007-160356@2x.png)

render 方法调用了ReactMount._renderSubtreeIntoContainer 方法，顾名思义，这个方法将一个组件渲染到dom中的特定容器（常用container）中，如果该React组件之前渲染过，该方法将执行它的更新，只在必要时（如数据更改时）对dom进行更改以显示最新状态，由于源码较长，有兴趣可以自己查阅，这里只列出结构：

```
_renderSubtreeIntoContainer: function(
    parentComponent,
    nextElement,
    container,
    callback,
  ) {
  ...
}
```

在经过一系列的处理，包括 container 对象，最后调用 _renderNewRootComponent 来生存一个 component 并返回。当然这其中还经历一些比如 DOMComponent 的创建，batchedUpdates 批量更新等。























