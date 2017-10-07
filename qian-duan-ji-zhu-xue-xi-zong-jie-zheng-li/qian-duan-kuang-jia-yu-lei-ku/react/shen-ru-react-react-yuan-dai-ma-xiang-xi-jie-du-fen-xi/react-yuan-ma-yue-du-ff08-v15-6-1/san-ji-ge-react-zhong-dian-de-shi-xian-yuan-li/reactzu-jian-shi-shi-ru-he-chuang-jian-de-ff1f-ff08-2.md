有了React元素对象还不能直接在浏览器中渲染，因为它不是一个标准的dom，还需要一个 render 过程，就是我们在React中写的 render() 方法，render方法的定义在src/renderers/dom/stack/client/ReactMount.js:

![](/assets/WX20171007-160356@2x.png)

render 方法调用了ReactMount._renderSubtreeIntoContainer 方法，顾名思义，这个方法将一个组件渲染到dom中的特定容器（常用container）中，如果该React组件之前渲染过，该方法将执行它的更新，只在必要时（如数据更改时）对dom进行更改以显示最新状态，源码如下：

```javascript
/**
 * @param {parentComponent} 父组件，对于第一次渲染，为null
 * @param {nextElement} 要插入到DOM中的组件，如<p>hi</p>经过babel转译后的元素
 * @param {container} 要插入到的容器，对应上面例子中的document.getElementById('example')获取的DOM对象
 * @param {callback} 第一次渲染为null
 *
 * @return {component}  返回ReactComponent，对于ReactDOM.render()调用，不用管返回值。
 */
_renderSubtreeIntoContainer: function(
    parentComponent,
    nextElement,
    container,
    callback,
  ) {
    //定义回调，后面执行
    callback = callback === undefined ? null : callback;
    
    if (__DEV__) {  ...  //此处省略部分__DEV__下的代码    }
    
    if (!React.isValidElement(nextElement)) {
      ...//一些报错提示，省略
    }

    warning(...//一些提示，省略);

    // 包装ReactElement，将nextElement挂载到wrapper的props属性下
    var nextWrappedElement = React.createElement(TopLevelWrapper, {
      child: nextElement,
    });

    var nextContext = getContextForSubtree(parentComponent);
    
    // 获取要插入到的容器的前一次的ReactComponent，这是为了做DOM diff
    var prevComponent = getTopLevelWrapperInContainer(container);

    if (prevComponent) {
      // 从prevComponent中获取到prevElement这个数据对象。
      var prevWrappedElement = prevComponent._currentElement;
      var prevElement = prevWrappedElement.props.child;
      
      // DOM diff 关键点之一，同一层级type和key不变时，只用update。否则先unmount再mount组件
      // 这里React为了避免递归太深，做了一个DOM diff前提假设，只对同一DOM层级，type相同，key(如果有)相同的组件做DOM diff，否则不比较，直接先unmount再mount。这个假设使diff算法复杂度从O(n^3)降低为O(n).
      // shouldUpdateReactComponent源码见后面分析
      if (shouldUpdateReactComponent(prevElement, nextElement)) {
        var publicInst = prevComponent._renderedComponent.getPublicInstance();
        var updatedCallback =
          callback &&
          function() {
            validateCallback(callback);
            callback.call(publicInst);
          };
          
        // 只需update，调用_updateRootComponent，然后直接return  
        ReactMount._updateRootComponent(
          prevComponent,
          nextWrappedElement,
          nextContext,
          container,
          updatedCallback,
        );
        return publicInst;
      } else {
      //不进行update，直接先卸载（unmountComponent）再挂载（mountComponent）。mountComponent在后面代码进行        
      ReactMount.unmountComponentAtNode(container);
      }
    }

    var reactRootElement = getReactRootElementInContainer(container);
    var containerHasReactMarkup =
      reactRootElement && !!internalGetID(reactRootElement);
    var containerHasNonRootReactChild = hasNonRootReactChild(container);

    if (__DEV__) { ...  //此处省略部分__DEV__下的代码   }

    var shouldReuseMarkup =
      containerHasReactMarkup &&
      !prevComponent &&
      !containerHasNonRootReactChild;
      
    // 渲染组件，然后插入到DOM中。_renderNewRootComponent很关键，后面具体分析
    var component = ReactMount._renderNewRootComponent(
      nextWrappedElement,
      container,
      shouldReuseMarkup,
      nextContext,
      callback,
    )._renderedComponent.getPublicInstance();
    
    return component;
  }
```


上面提到的两个关键方法：
shouldUpdateReactComponent()（源码定义在src/renderers/shared/shared/shouldUpdateReactComponent.js中）：


```javascript
function shouldUpdateReactComponent(prevElement, nextElement) {
  var prevEmpty = prevElement === null || prevElement === false;
  var nextEmpty = nextElement === null || nextElement === false;
  if (prevEmpty || nextEmpty) {
    return prevEmpty === nextEmpty;
  }

  var prevType = typeof prevElement;
  var nextType = typeof nextElement;
  
  // React DOM diff
  if (prevType === 'string' || prevType === 'number') {
     // 如果前后两次为数字或者字符,则认为只需要update(处理文本元素)，返回true
    return nextType === 'string' || nextType === 'number';
  } else {
     // 如果前后两次为DOM元素或React元素,则必须type和key不变(key用于listView等组件,很多时候我们没有设置key，故只需type相同)才update,否则先unmount再重新mount。返回false
    return (
      nextType === 'object' &&
      prevElement.type === nextElement.type &&
      prevElement.key === nextElement.key
    );
  }
}

```

另一个关键方法_renderNewRootComponent()（位置：src/renderers/shared/shared/ReactMount.js）：

```javascript
_renderNewRootComponent: function(
    nextElement,
    container,
    shouldReuseMarkup,
    context,
    callback,
  ) {
    warning(...);
    // 省略部分代码
    
    //注意这里
    ReactUpdates.batchedUpdates(
      batchedMountComponentIntoNode,
      componentInstance,
      container,
      shouldReuseMarkup,
      context,
    );

    var wrapperID = componentInstance._instance.rootID;
    instancesByReactRootID[wrapperID] = componentInstance;

    return componentInstance;
  }
```

上面代码中需要注意的是这里调用了ReactUpdates.batchedUpdates(），第一个参数传入的是batchedMountComponentIntoNode，这其实是ReactMount.js文件中定义的一个函数：

```
function batchedMountComponentIntoNode(
  componentInstance,
  container,
  shouldReuseMarkup,
  context,
) {
  var transaction = ReactUpdates.ReactReconcileTransaction.getPooled(
    !shouldReuseMarkup,
  );
  
  //注意这里
  transaction.perform(
    mountComponentIntoNode,
    null,
    componentInstance,
    container,
    transaction,
    shouldReuseMarkup,
    context,
  );
  ReactUpdates.ReactReconcileTransaction.release(transaction);
}

```

batchedMountComponentIntoNode中调用了transaction.perform()，里面传的第一个参数mountComponentIntoNode仍然是一个ReactMount.js里定义的函数：

```javascript
/**
 * 此方法作用是加载此组件并将其插入到dom中
 */
function mountComponentIntoNode(
  wrapperInstance,
  container,
  transaction,
  shouldReuseMarkup,
  context,
) {
  var markup = ReactReconciler.mountComponent(
    wrapperInstance,
    transaction,
    null,
    ReactDOMContainerInfo(wrapperInstance, container),
    context,
    0 /* parentDebugID */,
  );

  wrapperInstance._renderedComponent._topLevelWrapper = wrapperInstance;
  ReactMount._mountImageIntoNode(
    markup,
    container,
    wrapperInstance,
    shouldReuseMarkup,
    transaction,
  );
}

```





处理batchedMountComponentIntoNode方法调用，将ReactComponent插入DOM中

```
function batchedMountComponentIntoNode(
  componentInstance,
  container,
  shouldReuseMarkup,
  context,
) {
  var transaction = ReactUpdates.ReactReconcileTransaction.getPooled(
    /* useCreateElement */
    !shouldReuseMarkup,
  );
  transaction.perform(
    mountComponentIntoNode,
    null,
    componentInstance,
    container,
    transaction,
    shouldReuseMarkup,
    context,
  );
  ReactUpdates.ReactReconcileTransaction.release(transaction);
}

```


在经过一系列的处理，包括 container 对象，最后调用 _renderNewRootComponent 来生存一个 component 并返回。当然这其中还经历一些比如 DOMComponent 的创建，batchedUpdates 批量更新等。























