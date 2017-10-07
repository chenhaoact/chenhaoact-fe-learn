有了它还并不能直接在浏览器中渲染，因为还需要一个 render 过程，就是我们在React中写的 render() 方法，render方法的定义在src/renderers/dom/stack/client/ReactMount.js:

![](/assets/WX20171007-160356@2x.png)

render 方法调用了ReactMount._renderSubtreeIntoContainer 方法，来看源码：























