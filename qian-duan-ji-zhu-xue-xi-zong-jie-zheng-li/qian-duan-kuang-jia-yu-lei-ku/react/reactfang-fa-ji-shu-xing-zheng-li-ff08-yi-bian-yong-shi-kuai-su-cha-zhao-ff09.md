### 1 react方法及属性整理（以便用时快速查找）

（1）**React.createClass\(\)  创建一个react组件**（支持各种方法如render等，可作为react节点放到组件或页面中）

**React16版本中将会移除该方法。**（React.createClass is deprecated and will be removed in version 16. Use plain JavaScript classes instead. If you're not yet ready to migrate, create-react-class is available on npm as a drop-in replacement.）

（2）ReactDOM.render\(\)  渲染react元素到html节点上。实例化根组件，启动框架，注入标记到原始的 DOM 元素中。`ReactDOM`

模块暴露了 DOM 相关的方法， 而`React`保有被不同平台的 React 共享的核心工具 （例如[React Native](http://facebook.github.io/react-native/)）

（3）组件的render\(\)  react元素或组件的render函数定义组件要渲染的元素。该方法返回一颗** React 组件树，这棵树最终将会渲染成 HTML**。

