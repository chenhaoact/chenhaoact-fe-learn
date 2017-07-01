### 关于组件

组件就像是函数，可以认为React组件就是简单的函数，接受 props 和 state \(后面会讨论\) 作为参数，然后渲染出 HTML。

注意:只有一个限制: React 组件只能渲染单个根节点。如果你想要返回多个节点，它们必须被包含在同一个节点里。

#### （1）组件生命周期

**组件生命周期有三个主要部分：**

**挂载: 组件被注入DOM。**  
**更新: 组件被重新渲染来决定DOM是否应被更新。**  
**卸载: 组件从DOM中被移除。**

React提供生命周期方法，以便你可以指定钩挂到这个过程上。 will 方法在某事发生前被调用，did方法，在某事发生后被调用。

##### 1）挂载

getInitialState\(\): object 在组件**挂载前被调用**。**有状态组件应该实现此函数并返回初始state的数据**。

componentWillMount\(\) 在**挂载发生前被立即调用**。

componentDidMount\(\) 在**挂载发生后被立即调用。 需要DOM node的初始化应该放在这里**。

##### 2）更新

componentWillReceiveProps\(object nextProps\) **挂载的组件接收到新的props时被调用**。此方法应该被**用于比较this.props 和 nextProps以用于使用this.setState\(\)执行状态转换**。

shouldComponentUpdate\(object nextProps, object nextState\): boolean **当组件决定任何改变是否要更新到DOM时被调用**。作为一个优化实现**比较this.props 和 nextProps 、this.state 和 nextState **，如果React应该跳过更新，返回false。

componentWillUpdate\(object nextProps, object nextState\) 在**更新发生前被立即调用。你不能在此调用this.setState\(\)**。

componentDidUpdate\(object prevProps, object prevState\) 在**更新发生后被立即调用**。

##### 3）卸载

componentWillUnmount\(\) 在组件**被卸载和摧毁前被立即调用。清理应该放在这里。**

#### （2）把UI拆分为一个组件（或几个组件组合）的层级，要遵循组件功能单一原则

如何知道什么东西应该是独立的组件？一种这样的技术是[单一功能原则（single responsibility principle）](https://en.wikipedia.org/wiki/Single_responsibility_principle)，也就是一个组件在理想情况下只做一件事情。如果它最终增长了，它就应该被分解为更小的组件。

#### （3）Mixins （混合）

组件是 React 里复用代码的最佳方式，但**有时一些不同的组件间也需要共用一些功能。React 使用 mixins 来解决**这类问题。

一个通用的场景是：一个组件需要定期更新。用 setInterval\(\) 做很容易，但当不需要它的时候取消定时器来节省内存是非常重要的。React 提供 [生命周期方法](http://www.react-cn.com/docs/working-with-the-browser.html#component-lifecycle) 来告知你组件创建或销毁的时间。下面来做一个简单的 mixin，使用 setInterval\(\) 并保证在组件销毁时清理定时器。

```
//定义某个Mixin用于共用
var SetIntervalMixin = {
  componentWillMount: function() {
    this.intervals = [];
  },
  setInterval: function() {
    this.intervals.push(setInterval.apply(null, arguments));
  },
  componentWillUnmount: function() {
    this.intervals.forEach(clearInterval);
  }
};

var TickTock = React.createClass({
  mixins: [SetIntervalMixin], // ！注意这里，引用 mixin ！
  getInitialState: function() {
    return {seconds: 0};
  },
  componentDidMount: function() {
    this.setInterval(this.tick, 1000); // 调用 mixin 的方法
  },
  tick: function() {
    this.setState({seconds: this.state.seconds + 1});
  },
  render: function() {
    return (
      <p>
        React has been running for {this.state.seconds} seconds.
      </p>
    );
  }
});

ReactDOM.render(
  <TickTock />,
  document.getElementById('example')
);
```

关于 mixin 值得一提的优点是，**如果一个组件使用了多个 mixin，并用有多个 mixin 定义了同样的生命周期方法**（如：多个 mixin 都需要在组件销毁时做资源清理操作），所有这些生命周期方法都保证会被执行到。**方法执行顺序是：首先按 mixin 引入顺序执行 mixin 里方法，最后执行组件内定义的方法。**

不幸的是ES6的发布没有任何mixin的支持。因此，当你在ES6 classes下使用React时不支持mixins。作为替代，我们正在努力使它更容易不依靠mixins支持这些用例。

#### （4）用ES6 Classes生成react组件

也可以以一个简单的 JavaScript 类来定义你的React classes。使用ES6 class的例子:

```
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}
```

##### class 组件名 extends React.Component和React.createClass的区别：

**1）API近似于 React.createClass 除了 getInitialState。应该在构造函数里设置你的state**，而不是提供一个单独的 getInitialState 方法。就像 getInitialState 的返回值，你**赋给 this.state 的值会被作为组件的初始 state**。

**2）propTypes 和 defaultProps 是在构造函数里被定义为属性，而不是在 class body 里**。

```
export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return (
      <div onClick={this.tick.bind(this)}>
        Clicks: {this.state.count}
      </div>
    );
  }
}
Counter.propTypes = { initialCount: React.PropTypes.number };
Counter.defaultProps = { initialCount: 0 };
```

**3）不会自动绑定this到实例上。你必须显示的使用.bind\(this\) or 箭头函数 =&gt;：**

    // 你可以使用 bind() 来绑定 `this`
    <div onClick={this.tick.bind(this)}>

    // 或者你可以使用箭头函数
    <div onClick={() => this.tick()}>

**建议向下面这样在构造函数中绑定事件处理器，这样对于所有实例它们只需绑定一次,这对应用的性能有帮助，特别是当你用 浅层比较 实现 shouldComponentUpdate\(\) 时：**

```
constructor(props) {
  super(props);
  this.state = {count: props.initialCount};
  this.tick = this.tick.bind(this);
}
```

现在就可以直接使用 this.tick 因为它已经在构造函数里绑定过一次了：

```
// 它已经在构造函数里绑定过了
<div onClick={this.tick}>
```

**4）没有 Mixins**  
不幸的是ES6的发布没有任何mixin的支持。因此，当你在ES6 classes下使用React时不支持mixins。作为替代，我们正在努力使它更容易不依靠mixins支持这些用例。

**可以使用js的无状态函数（可以带props,但不要有state），这里建议使用新的ES6箭头函数的写法:**

```
const HelloMessage = (props) => <div>Hello {props.name}</div>;

ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);
```

**这个简化的组件API旨在用于那些纯函数态的组件 。这些组件必须没有保持任何内部状态，没有备份实例，也没有组件生命周期方法。**他们纯粹的函数式的转化他们的输入，没有引用。 然而，你**仍然可以以设置函数 properties 的方式来指定 .propTypes 和 .defaultProps**，就像你在ES6类里设置他们那样。

注意：

因为无状态函数没有备份实例，你不能附加一个引用到一个无状态函数组件。 通常这不是问题，因为无状态函数不提供一个命令式的API。没有命令式的API，你就没有任何需要实例来做的事。然而，如果用户想查找无状态函数组件的DOM节点，他们必须把这个组件包装在一个有状态组件里（比如，ES6 类组件） 并且连接一个引用到有状态的包装组件。

**在理想世界里，你的大多数组件都应该是无状态函数，因为将来我们可能会用避免不必要的检查和内存分配的方式来对这些组件进行优化。 如果可能，这是推荐的模式**。

