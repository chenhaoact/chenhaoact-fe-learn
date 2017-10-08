**合成事件（SyntheticEvent）系统**是React一个比较重要的部分，它兼容性很好，同时能够提升页面性能，那么合成事件系统在源码中是如何实现的呢？

从用户的交互触发一个事件后，主要要经过事件注册与分发，事件的执行，事件的存储与销毁等过程。

比如我们在jsx中给一个按钮绑定一个onClick事件：



```
<button onClick = { this.onBtnClick.bind(this) } />
```

这段代码在React组件创建和更新的方法mountComponent和updateComponent中，会调用_updateDOMProperties方法来处理。

这里以ReactDOMComponent.js为例（位置：src/renderers/dom/stack/client/ReactDOMComponent.js）:

![](/assets/WX20171008-175539@2x.png)

可以看到这里的mountComponent中调用了_updateDOMProperties，它会对JSX中声明的组件属性进行处理，其中会调用到一个ensureListeningTo方法，这个方法很关键，负责注册JSX中声明的事件，来看源码（位置：src/renderers/dom/stack/client/ReactDOMComponent.js）：



```
function ensureListeningTo(inst, registrationName, transaction) {
  if (transaction instanceof ReactServerRenderingTransaction) {
    return;
  }
  var containerInfo = inst._hostContainerInfo;
  var isDocumentFragment =
    containerInfo._node &&
    containerInfo._node.nodeType === DOCUMENT_FRAGMENT_NODE;
  var doc = isDocumentFragment
    ? containerInfo._node
    : containerInfo._ownerDocument;
  listenTo(registrationName, doc);
}
```



















