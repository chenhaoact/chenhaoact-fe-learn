
### 装载组件触发 （componentWillMount，componentDidMount）
componentWillMount（只会在装载之前调用一次，在 render 前调用，可以在这个方法里面调用 setState 改变状态，并且不会导致额外调用一次 render），render，componentDidMount（在装载完成之后调用一次，在 render 后调用，从这里开始可以通过 ReactDOM.findDOMNode(this) 获取到组件的 DOM 节点）都是在mountComponent中被调用。

不同的React组件的mountComponent实现都有所区别（之前提过有多种ReactElement）。这里以ReactCompositeComponent的mountComponent为例说明（代码位置：src/renderers/shared/stack/reconciler/ReactCompositeComponent.js）：

```javascript
mountComponent: function(
    transaction,
    hostParent,
    hostContainerInfo,
    context,
  ) {
    this._context = context;
    this._mountOrder = nextMountID++;
    this._hostParent = hostParent;
    this._hostContainerInfo = hostContainerInfo;

    var publicProps = this._currentElement.props;
    var publicContext = this._processContext(context);

    var Component = this._currentElement.type;

    var updateQueue = transaction.getUpdateQueue();

    var doConstruct = shouldConstruct(Component);
    var inst = this._constructComponent(
      doConstruct,
      publicProps,
      publicContext,
      updateQueue,
    );
    var renderedElement;

    if (!doConstruct && (inst == null || inst.render == null)) {
      renderedElement = inst;
      if (__DEV__) { ... }
      invariant( ... );
      inst = new StatelessComponent(Component);
      this._compositeType = ReactCompositeComponentTypes.StatelessFunctional;
    } else {
      if (isPureComponent(Component)) {
        this._compositeType = ReactCompositeComponentTypes.PureClass;
      } else {
        this._compositeType = ReactCompositeComponentTypes.ImpureClass;
      }
    }

    if (__DEV__) { ... }

      var propsMutated = inst.props !== publicProps;
      var componentName =
        Component.displayName || Component.name || 'Component';

      warning( ... );
    }

    inst.props = publicProps;
    inst.context = publicContext;
    inst.refs = emptyObject;
    inst.updater = updateQueue;

    this._instance = inst;

    ReactInstanceMap.set(inst, this);

    if (__DEV__) { ... }

    // 这里设置了 initialState
    var initialState = inst.state;
    if (initialState === undefined) {
      inst.state = initialState = null;
    }
    invariant( ... );

    this._pendingStateQueue = null;
    this._pendingReplaceState = false;
    this._pendingForceUpdate = false;

    if (inst.componentWillMount) {
      if (__DEV__) {
        measureLifeCyclePerf(
          () => inst.componentWillMount(),
          this._debugID,
          'componentWillMount',
        );
      } else {
        // 这里执行了componentWillMount()
        inst.componentWillMount();
      }
      
      if (this._pendingStateQueue) {
        inst.state = this._processPendingState(inst.props, inst.context);
      }
    }

    var markup;
    if (inst.componentDidCatch) {
      markup = this.performInitialMountWithErrorHandling(
        renderedElement,
        hostParent,
        hostContainerInfo,
        transaction,
        context,
      );
    } else {
      markup = this.performInitialMount(
        renderedElement,
        hostParent,
        hostContainerInfo,
        transaction,
        context,
      );
    }

    if (inst.componentDidMount) {
      if (__DEV__) {
        transaction.getReactMountReady().enqueue(() => {
          measureLifeCyclePerf(
            () => inst.componentDidMount(),
            this._debugID,
            'componentDidMount',
          );
        });
      } else {
     // 这里执行了 componentDidMount       transaction.getReactMountReady().enqueue(inst.componentDidMount, inst);
      }
    }

    //在willMount执行的 setState的回调函数会在这里调用
    const callbacks = this._pendingCallbacks;
    if (callbacks) {
      this._pendingCallbacks = null;
      for (let i = 0; i < callbacks.length; i++) {
        transaction.getReactMountReady().enqueue(callbacks[i], inst);
      }
    }

    return markup;
  }

```

### 更新组件触发（componentWillReceiveProps，shouldComponentUpdate，componentWillUpdate，componentDidUpdate）
这些方法不会在首次 render 组件的周期调用，当组件的状态发生变化时（比如通过setState修改了组件的state）会触发组件的更新，这些逻辑会在updateComponent中调用，也就是说组件更新的逻辑主要是在updateComponent方法中。

仍然以ReactCompositeComponent的updateComponent方法为例（代码位置：src/renderers/shared/stack/reconciler/ReactCompositeComponent.js）：



```javascript
updateComponent: function(
    transaction,
    prevParentElement,
    nextParentElement,
    prevUnmaskedContext,
    nextUnmaskedContext,
  ) {
    var inst = this._instance;
    invariant( ... );

    var willReceive = false;
    var nextContext;

    if (this._context === nextUnmaskedContext) {
      nextContext = inst.context;
    } else {
      nextContext = this._processContext(nextUnmaskedContext);
      willReceive = true;
    }

    var prevProps = prevParentElement.props;
    var nextProps = nextParentElement.props;

    // Not a simple state update but a props update
    if (prevParentElement !== nextParentElement) {
      willReceive = true;
    }

    if (willReceive && inst.componentWillReceiveProps) {
      const beforeState = inst.state;
      if (__DEV__) {
        ...
      } else {
    // 这里调用了componentWillReceiveProps(）       inst.componentWillReceiveProps(nextProps, nextContext);
      }
      const afterState = inst.state;
      if (beforeState !== afterState) {
        inst.state = beforeState;
        inst.updater.enqueueReplaceState(inst, afterState);
        if (__DEV__) {
         ...
        }
      }
    }

    var callbacks = this._pendingCallbacks;
    this._pendingCallbacks = null;

    var nextState = this._processPendingState(nextProps, nextContext);
    var shouldUpdate = true;
    if (!this._pendingForceUpdate) {
      var prevState = inst.state;
      shouldUpdate = willReceive || nextState !== prevState;
      if (inst.shouldComponentUpdate) {
        if (__DEV__) {
          ...
        } else {
        //这里用到了shouldComponentUpdate
          shouldUpdate = inst.shouldComponentUpdate(
            nextProps,
            nextState,
            nextContext,
          );
        }
      } else {
        if (this._compositeType === ReactCompositeComponentTypes.PureClass) {
          shouldUpdate =
            !shallowEqual(prevProps, nextProps) ||
            !shallowEqual(inst.state, nextState);
        }
      }
    }

    if (__DEV__) {
      ...
    }

    this._updateBatchNumber = null;
    
    //如果shouldUpdate为true,则执行更新渲染
    if (shouldUpdate) {
      this._pendingForceUpdate = false;
      // 执行更新渲染的逻辑
      this._performComponentUpdate(
        nextParentElement,
        nextProps,
        nextState,
        nextContext,
        transaction,
        nextUnmaskedContext,
      );
    } else {
      this._currentElement = nextParentElement;
      this._context = nextUnmaskedContext;
      inst.props = nextProps;
      inst.state = nextState;
      inst.context = nextContext;
    }

    if (callbacks) {
      for (var j = 0; j < callbacks.length; j++) {
        transaction
          .getReactMountReady()
          .enqueue(callbacks[j], this.getPublicInstance());
      }
    }
  }

```

通过上面代码可以看出，updateComponent中执行了componentWillReceiveProps和shouldComponentUpdate逻辑，最后shouldUpdate为true进行更新渲染时调用的是   _performComponentUpdate，来看
_performComponentUpdate的源码(位置同上)：



```javascript
_performComponentUpdate: function(
    nextElement,
    nextProps,
    nextState,
    nextContext,
    transaction,
    unmaskedContext,
  ) {
    var inst = this._instance;

    var hasComponentDidUpdate = !!inst.componentDidUpdate;
    var prevProps;
    var prevState;
    if (hasComponentDidUpdate) {
      prevProps = inst.props;
      prevState = inst.state;
    }

    if (inst.componentWillUpdate) {
      if (__DEV__) {
        ...
      } else {
      // 这里执行了componentWillUpdate
        inst.componentWillUpdate(nextProps, nextState, nextContext);
      }
    }

    // 重新设置state props等属性
    this._currentElement = nextElement;
    this._context = unmaskedContext;
    inst.props = nextProps;
    inst.state = nextState;
    inst.context = nextContext;

    if (inst.componentDidCatch) {
      this._updateRenderedComponentWithErrorHandling(
        transaction,
        unmaskedContext,
      );
    } else {
      // 调用render方法，重新解析ReactElement并得到HTML
      this._updateRenderedComponent(transaction, unmaskedContext);
    }

    if (hasComponentDidUpdate) {
      if (__DEV__) {
        ...
      } else {
        // 这里执行了componentDidUpdate
        transaction
          .getReactMountReady()
          .enqueue(
            inst.componentDidUpdate.bind(inst, prevProps, prevState),
            inst,
          );
      }
    }
  }
```

可以看到_performComponentUpdate中执行了componentWillUpdate（更新render前），componentDidUpdate（更新render后），至此，更新组件触发的生命周期函数就齐了。


### 卸载组件触发（componentWillUnmount）
卸载组件时，主要的逻辑是在unmountComponent方法（更新组件时如果不满足DOM diff条件，也会先unmountComponent, 然后再mountComponent。），来看下unmountComponent源码（以ReactCompositeComponent为例，位置同上）：


```javascript
unmountComponent: function(safely, skipLifecycle) {
    if (!this._renderedComponent) {
      return;
    }

    var inst = this._instance;

    if (inst.componentWillUnmount && !inst._calledComponentWillUnmount) {
      inst._calledComponentWillUnmount = true;

      if (safely) {
        if (!skipLifecycle) {
          var name = this.getName() + '.componentWillUnmount()';
          ReactErrorUtils.invokeGuardedCallbackAndCatchFirstError(
            name,
            inst.componentWillUnmount,
            inst,
          );
        }
      } else {
        if (__DEV__) {
          ...
        } else {
          // 这里执行了componentWillUnmount
          inst.componentWillUnmount();
        }
      }
    }

    // 递归调用unMountComponent来销毁子组件
    if (this._renderedComponent) {
      ReactReconciler.unmountComponent(
        this._renderedComponent,
        safely,
        skipLifecycle,
      );
      this._renderedNodeType = null;
      this._renderedComponent = null;
      this._instance = null;
    }

    //将一些内部变量置空，防止内存泄漏
    this._pendingStateQueue = null;
    this._pendingReplaceState = false;
    this._pendingForceUpdate = false;
    this._pendingCallbacks = null;
    this._pendingElement = null;

    this._context = null;
    this._rootNodeID = 0;
    this._topLevelWrapper = null;

    ReactInstanceMap.remove(inst);
  }

```

可以看到在unmountComponent里调用componentWillUnmount()，然后递归调用unmountComponent(),最后销毁子组件将内部变量置空，防止内存泄漏。

至此，React的生命周期就基本能理清了，其他几种类型的React Component也类似，这里不在赘述，有兴趣可以看下源码。








