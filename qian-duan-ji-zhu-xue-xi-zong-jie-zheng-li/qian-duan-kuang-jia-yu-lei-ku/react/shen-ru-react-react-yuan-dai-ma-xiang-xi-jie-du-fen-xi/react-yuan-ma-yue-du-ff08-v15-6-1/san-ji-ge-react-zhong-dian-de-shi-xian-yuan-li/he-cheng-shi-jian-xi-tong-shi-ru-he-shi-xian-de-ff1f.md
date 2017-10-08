**合成事件（SyntheticEvent）系统**是React一个比较重要的部分，它兼容性很好，同时能够提升页面性能，那么合成事件系统在源码中是如何实现的呢？

从用户的交互触发一个事件后，主要要经过事件注册，分发，执行，销毁等过程。

### 事件绑定
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
  // 找到document
  var containerInfo = inst._hostContainerInfo;
  var isDocumentFragment =
    containerInfo._node &&
    containerInfo._node.nodeType === DOCUMENT_FRAGMENT_NODE;
  var doc = isDocumentFragment
    ? containerInfo._node
    : containerInfo._ownerDocument;
  
  // 将事件注册到document上  
  listenTo(registrationName, doc);
}
```

这里通过listenTo方法将事件注册到document这个原生dom节点上，该方法解决了不同浏览器间捕获和冒泡不兼容的问题，来看源码（位置 src/renderers/dom/shared/ReactBrowserEventEmitter.js）：

```javascript
listenTo: function(registrationName, contentDocumentHandle) {
    var mountAt = contentDocumentHandle;
    var isListening = getListeningForDocument(mountAt);
    var dependencies =
      EventPluginRegistry.registrationNameDependencies[registrationName];

    for (var i = 0; i < dependencies.length; i++) {
      var dependency = dependencies[i];
      if (
        !(isListening.hasOwnProperty(dependency) && isListening[dependency])
      ) {
        if (dependency === 'topWheel') {
          if (isEventSupported('wheel')) {
            // 使用trapBubbledEvent() 注册事件冒泡
            ReactDOMEventListener.trapBubbledEvent(
              'topWheel',
              'wheel',
              mountAt,
            );
          } else if (isEventSupported('mousewheel')) {
            ReactDOMEventListener.trapBubbledEvent(
              'topWheel',
              'mousewheel',
              mountAt,
            );
          } else {
            ReactDOMEventListener.trapBubbledEvent(
              'topWheel',
              'DOMMouseScroll',
              mountAt,
            );
          }
        } else if (dependency === 'topScroll') {
          // 使用trapBubbledEvent() 注册事件捕获
          ReactDOMEventListener.trapCapturedEvent(
            'topScroll',
            'scroll',
            mountAt,
          );
        } else if (dependency === 'topFocus' || dependency === 'topBlur') {
          ReactDOMEventListener.trapCapturedEvent('topFocus', 'focus', mountAt);
          ReactDOMEventListener.trapCapturedEvent('topBlur', 'blur', mountAt);

          isListening.topBlur = true;
          isListening.topFocus = true;
        } else if (dependency === 'topCancel') {
          if (isEventSupported('cancel', true)) {
            ReactDOMEventListener.trapCapturedEvent(
              'topCancel',
              'cancel',
              mountAt,
            );
          }
          isListening.topCancel = true;
        } else if (dependency === 'topClose') {
          if (isEventSupported('close', true)) {
            ReactDOMEventListener.trapCapturedEvent(
              'topClose',
              'close',
              mountAt,
            );
          }
          isListening.topClose = true;
        } else if (topLevelTypes.hasOwnProperty(dependency)) {
          ReactDOMEventListener.trapBubbledEvent(
            dependency,
            topLevelTypes[dependency],
            mountAt,
          );
        }

        isListening[dependency] = true;
      }
    }
  }
```

可以看到这里频繁的使用了ReactDOMEventListener.trapBubbledEvent()和ReactDOMEventListener.trapCapturedEvent()两个方法，它们分别是用来注册事件捕获和事件冒泡的，源码如下（位置 src/renderers/dom/shared/ReactDOMEventListener.js）：



```javascript
  /**
   * Traps top-level events by using event bubbling.
   */
  trapBubbledEvent: function(topLevelType, handlerBaseName, element) {
    if (!element) {
      return null;
    }
    return EventListener.listen(
      element,
      handlerBaseName,
      //用ReactDOMEventListener.dispatchEvent()进行事件分发，后面说明
      ReactDOMEventListener.dispatchEvent.bind(null, topLevelType),
    );
  },

  /**
   * Traps a top-level event by using event capturing.
   */
  trapCapturedEvent: function(topLevelType, handlerBaseName, element) {
    if (!element) {
      return null;
    }
    return EventListener.capture(
      element,
      handlerBaseName,
      //用ReactDOMEventListener.dispatchEvent()进行事件分发，后面说明
      ReactDOMEventListener.dispatchEvent.bind(null, topLevelType),
    );
  },

```

这里 trapBubbledEvent 返回的是EventListener.listen()，trapCapturedEvent 返回的是EventListener.capture()，这里的EventListener引用自fbjs/lib/EventListener模块，去（node_modules/fbjs/lib/EventListener.js）看下源码：



```javascript
listen: function listen(target, eventType, callback) {
    if (target.addEventListener) {
      
      //调用了addEventListener()
      target.addEventListener(eventType, callback, false);
      return {
        remove: function remove() {
          
          //调用了removeEventListener()
          target.removeEventListener(eventType, callback, false);
        }
      };
    } else if (target.attachEvent) {
      target.attachEvent('on' + eventType, callback);
      return {
        remove: function remove() {
          target.detachEvent('on' + eventType, callback);
        }
      };
    }
  },

  /**
   * Listen to DOM events during the capture phase.
   */
  capture: function capture(target, eventType, callback) {
    if (target.addEventListener) {
      target.addEventListener(eventType, callback, true);
      return {
        remove: function remove() {
          target.removeEventListener(eventType, callback, true);
        }
      };
    } else {
      if (process.env.NODE_ENV !== 'production') {
        console.error('Attempted to listen to events during the capture phase on a ' + 'browser that does not support the capture phase. Your application ' + 'will not receive some events.');
      }
      return {
        remove: emptyFunction
      };
    }
  }

```
**这里可以看到熟悉的原生js的addEventListener和removeEventListener方法，正是在这里将原生的js事件注册到页面的dom上的。**

### 事件分发
上面代码里提到过ReactDOMEventListener.trapBubbledEvent()和ReactDOMEventListener.trapCapturedEvent()两个方法中都使用ReactDOMEventListener.dispatchEvent()进行事件分发，源码如下：



```
// nativeEvent是用户触发事件时，浏览器传递的原生事件（如click）
dispatchEvent: function(topLevelType, nativeEvent) {
    if (!ReactDOMEventListener._enabled) {
      return;
    }

    var nativeEventTarget = getEventTarget(nativeEvent);
    var targetInst = ReactDOMComponentTree.getClosestInstanceFromNode(
      nativeEventTarget,
    );
    if (
      targetInst !== null &&
      typeof targetInst.tag === 'number' &&
      !ReactFiberTreeReflection.isFiberMounted(targetInst)
    ) {
      targetInst = null;
    }

    var bookKeeping = getTopLevelCallbackBookKeeping(
      topLevelType,
      nativeEvent,
      targetInst,
    );

    try {
   // 注意这里 ReactGenericBatching.batchedUpdates(handleTopLevelImpl, bookKeeping);
    } finally {
      releaseTopLevelCallbackBookKeeping(bookKeeping);
    }
  }

```

dispatchEvent方法中将handleTopLevelImpl放入执行了ReactGenericBatching.batchedUpdates()进行批处理，实际的事件分发逻辑写在handleTopLevelImpl中：

```
function handleTopLevelImpl(bookKeeping) {
  // 找到事件触发的dom元素和React Component实例
  var targetInst = bookKeeping.targetInst;
  var ancestor = targetInst;
  do {
    if (!ancestor) {
      bookKeeping.ancestors.push(ancestor);
      break;
    }
    var root = findRootContainerNode(ancestor);
    if (!root) {
      break;
    }
    bookKeeping.ancestors.push(ancestor);
    ancestor = ReactDOMComponentTree.getClosestInstanceFromNode(root);
  } while (ancestor);

  //从当前组件向父组件遍历,依次执行注册的回调方法
  for (var i = 0; i < bookKeeping.ancestors.length; i++) {
    targetInst = bookKeeping.ancestors[i];
    ReactDOMEventListener._handleTopLevel(
      bookKeeping.topLevelType,
      targetInst,
      bookKeeping.nativeEvent,
      getEventTarget(bookKeeping.nativeEvent),
    );
  }
}

```

上面代码让React自身实现了一套冒泡机制，遍历中执行的顺序就是冒泡的顺序,因此在React中不能通过stopPropagation来阻止冒泡。

事件系统还有不少复杂的逻辑，这里暂时不展开去看，有兴趣可以阅读源码研究。




