组件化的开发是React的特点之一，通过组件,既能够提升开发效率，也让项目的可维护性更高。
开发中，可以使用React.createClass()（ES5写法）或class myComponent extends React.Component（ES6，内部也是调用createClass）来创建组件。

createClass主要做的事情有定义构造方法constructor，构造方法中进行props，refs等的初始化，并调用getInitialState来初始化state等.

目前createClass已经在16版本中被分离出来，可以通过安装npm包 create-react-class 来使用。

### React 元素的构建

定义一个ReactElement对象用到的ReactElement方法源码如下：

```
var ReactElement = function(type, key, ref, self, source, owner, props) {
  var element = {
    // 通过此标签标识这是一个React Element
    $$typeof: REACT_ELEMENT_TYPE,

    // 创建React元素的基本属性
    type: type,
    key: key,
    ref: ref,
    props: props,

    // 记录此元素的拥有者（那个组件创建了这个元素）
    _owner: owner,
  };

  //开发环境下的一些处理，方便调试与测试
  if (__DEV__) {
    element._store = {};
    Object.defineProperty(element._store, 'validated', {
      configurable: false,
      enumerable: false,
      writable: true,
      value: false,
    });
    
    Object.defineProperty(element, '_self', {
      configurable: false,
      enumerable: false,
      writable: false,
      value: self,
    });
    
    Object.defineProperty(element, '_source', {
      configurable: false,
      enumerable: false,
      writable: false,
      value: source,
    });
    if (Object.freeze) {
      Object.freeze(element.props);
      Object.freeze(element);
    }
  }

  return element;
};

```

在ReactElement对象上定义了很多方法，如createElement，cloneAndReplaceKey，cloneElement等，其中通过createElement方法来创建一个React元素，源码如下：

```
ReactElement.createElement = function(type, config, children) {
  var propName;

  // 初始化
  var props = {};

  var key = null;
  var ref = null;
  var self = null;
  var source = null;

  // 如果config存在，从config中提取出ref key props等属性
  if (config != null) {
    if (hasValidRef(config)) {
      ref = config.ref;
    }
    if (hasValidKey(config)) {
      key = '' + config.key;
    }

    self = config.__self === undefined ? null : config.__self;
    source = config.__source === undefined ? null : config.__source;
    // Remaining properties are added to a new props object
    for (propName in config) {
      if (
        hasOwnProperty.call(config, propName) &&
        !RESERVED_PROPS.hasOwnProperty(propName)
      ) {
        props[propName] = config[propName];
      }
    }
  }
  
  // 处理children参数，挂载到props的children属性下
  var childrenLength = arguments.length - 2;
  if (childrenLength === 1) {
    props.children = children;
  } else if (childrenLength > 1) {
    var childArray = Array(childrenLength);
    for (var i = 0; i < childrenLength; i++) {
      childArray[i] = arguments[i + 2];
    }
    if (__DEV__) {
      if (Object.freeze) {
        Object.freeze(childArray);
      }
    }
    props.children = childArray;
  }

  // 取出组件类中的静态变量defaultProps，并给未设置值的属性设置默认值
  if (type && type.defaultProps) {
    var defaultProps = type.defaultProps;
    for (propName in defaultProps) {
      if (props[propName] === undefined) {
        props[propName] = defaultProps[propName];
      }
    }
  }
  if (__DEV__) {
    if (key || ref) {
      if (
        typeof props.$$typeof === 'undefined' ||
        props.$$typeof !== REACT_ELEMENT_TYPE
      ) {
        var displayName = typeof type === 'function'
          ? type.displayName || type.name || 'Unknown'
          : type;
        if (key) {
          defineKeyPropWarningGetter(props, displayName);
        }
        if (ref) {
          defineRefPropWarningGetter(props, displayName);
        }
      }
    }
  }
  
  // 最后返回一个ReactElement对象
  return ReactElement(
    type,
    key,
    ref,
    self,
    source,
    ReactCurrentOwner.current,
    props,
  );
};

```

我们用JSX语法写的代码，比如：



```
<div className="cls" ref="div1">
    <p>hi</p>    // 原生DOM组件，首字母小写
    <A title='yo' data={'data1'}/>    // 自定义组件，首字母大写
</div>
```


会被转化为：


```
React.createElement(
        // type,标签名
        'div',   
        // config，属性
        {        
            className: 'cls',
            ref: 'div1'
        },
        // children  子元素 ，这里有两个
        React.createElement('p', null, 'hi'),   
        React.createElement(
            // type,标签名,React自定义组件的type不为String.
            // _a.default为从其他文件中引入的React组件
            _a.default,    
            {
                title: 'yo',
                data: 'data1'
            }
        )  
)
```

最后通过上面的createElement方法的处理，变为这样的一个对象：

```
{
    $$typeof: (typeof Symbol === 'function' && Symbol.for && Symbol.for('react.element')) ||
  0xeac7,
    type: 'div',
    key: null,
    ref: 'div1',
    props: {
        className: 'cls',
        children: [
            {
                $$typeof: (typeof Symbol === 'function' && Symbol.for && Symbol.for('react.element')) ||
  0xeac7,
                  type: 'p',
                  key: null,
                  ref: null,
                  props: {
                      className: null,
                      children: [] || object // 如果你的子节点只有一个，children将不适数组而是一个对象
                  },
                  _owner: null
            },
            {
              ... //第二个子元素A
            }
        ]
    },
    _owner: null
}
```

内容较长，分成几节，接到：
[React组件是如何创建的？（2）](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/qian-duan-kuang-jia-yu-lei-ku/react/shen-ru-react-react-yuan-dai-ma-xiang-xi-jie-du-fen-xi/react-yuan-ma-yue-du-ff08-v15-6-1/san-ji-ge-react-zhong-dian-de-shi-xian-yuan-li/reactzu-jian-shi-shi-ru-he-chuang-jian-de-ff1f-ff08-2.md)






















