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
