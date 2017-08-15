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

### 常用实例

#### 1）tab切换 - （子组件各自的componentDidMount()里）
一个页面中tab切换 tab1,tab2组件，每次切换到某tab时，tab1或tab2的 render() 每次都会执行，而componentDidMount() 只会在 该tab 第一次被切换到 加载时执行，以后再切换不会重复去执行，所以 发请求获取默认数据的操作可以放在 子组件各自的componentDidMount()里
