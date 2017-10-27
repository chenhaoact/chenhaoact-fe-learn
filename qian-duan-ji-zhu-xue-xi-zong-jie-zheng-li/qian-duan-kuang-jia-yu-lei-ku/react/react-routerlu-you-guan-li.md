# React-router-路由管理

## 一 简介

### 1用途
####（1）适用场景


### 2优缺点及对比
####（1）优点

####（2）缺点


## 二 基本概念与技术重点整理

React项目通常都有很多的URL需要管理，最常使用的解决方案就是React Router了，最近学习了一下，主要是看了一下官方的英文文档，加以总结，以备后查。

React Router是做什么的呢，官方的介绍是：

A complete routing library for React，keeps your UI in sync with the URL. It has a simple API with powerful features like lazy code loading, dynamic route matching, and location transition handling built right in. Make the URL your first thought, not an after-thought.

大意即：让UI组件和URL保持同步,通过简单的API即可实现强大的特性如：代码懒加载，动态路由匹配，路径过渡处理等。


下面是一些React Router的用法：

##一 简单渲染Route

有一点需要牢记于心，Router 是作为一个React组件，可以进行渲染。

```
// ...
import { Router, Route, hashHistory } from 'react-router'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
  </Router>
), document.getElementById('app'))
```

这里使用了hashHistory - 它管理路由历史与URL的哈希部分。
添加更多的路由，并指定它们对应的组件

```
import About from './modules/About'
import Repos from './modules/Repos'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
    <Route path="/repos" component={Repos}/>
    <Route path="/about" component={About}/>
  </Router>
), document.getElementById('app'))
```

##二 Link

```
// modules/App.js
import React from 'react'
import { Link } from 'react-router'

export default React.createClass({
  render() {
    return (
      <div>
        <h1>React Router Tutorial</h1>
        <ul role="nav">
          <li><Link to="/about">About</Link></li>
          <li><Link to="/repos">Repos</Link></li>
        </ul>
      </div>
    )
  }
})
```

这里使用了Link 组件，它可以渲染出链接并使用 to 属性指向相应的路由。

##三 嵌套路由

如果我们想添加一个导航栏，需要存在于每个页面上。如果没有路由器，我们就需要封装一个一个nav组件，并在每一个页面组件都引用和渲染。随着应用程序的增长代码会显得很冗余。React-router则提供了另一种方式来嵌套共享UI组件。

实际上，我们的app都是一系列嵌套的盒子，对应的url也能够说明这种嵌套关系：

```
<App>       {/* url  /          */}
  <Repos>   {/* url  /repos     */}
    <Repo/> {/* url  /repos/123 */}
  </Repos>
</App>
```

因此，可以通过把子组件嵌套到 公共组件 App上使得 App组件上的 导航栏 Nav 等公共部分能够共享：

```
// index.js
// ...
render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>
      {/* 注意这里把两个子组件放在Route里嵌套在了App的Route里/}
      <Route path="/repos" component={Repos}/>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))
```

接下来，在App中将children渲染出来：

```
// modules/App.js
// ...
  render() {
    return (
      <div>
        <h1>React Router Tutorial</h1>
        <ul role="nav">
          <li><Link to="/about">About</Link></li>
          <li><Link to="/repos">Repos</Link></li>
        </ul>

        {/* 注意这里将子组件渲染出来 */}
        {this.props.children}

      </div>
    )
  }
// ...
```

##四 有效链接

Link组件和a标签的不同点之一就在于Link可以知道其指向的路径是否是一个有效的路由。

```
<li><Link to="/about" activeStyle={{ color: 'red' }}>About</Link></li>
<li><Link to="/repos" activeStyle={{ color: 'red' }}>Repos</Link></li>
```

可以使用 activeStyle 指定有效链接的样式，也可以使用activeClassName指定有效链接的样式类。

大多数时候，我们并不需要知道链接是否有效，但在导航中这个特性则十分重要。比如：可以在导航栏中只显示合法的路由链接。

```
// modules/NavLink.js
import React from 'react'
import { Link } from 'react-router'

export default React.createClass({
  render() {
    return <Link {...this.props} activeClassName="active"/>
  }
})
```

```
// modules/App.js
import NavLink from './NavLink'

// ...

<li><NavLink to="/about">About</NavLink></li>
<li><NavLink to="/repos">Repos</NavLink></li>
```

可以在NavLink中指定只有 .active 的链接才显示，这样如果路由无效，则该链接就不会出现在导航栏中了。


##五 URL参数

考虑下面的url：

/repos/reactjs/react-router
/repos/facebook/react

他们可能对应的是这种形式：

/repos/:userName/:repoName


：后面是可变的参数

url中的可变参数可以通过 this.props.params[paramsName] 获取到：

```
// modules/Repo.js
import React from 'react'

export default React.createClass({
  render() {
    return (
      <div>
{/* 注意这里通过this.props.params.repoName 获取到url中的repoName参数的值 */}
        <h2>{this.props.params.repoName}</h2>
      </div>
    )
  }
})
```

```
// index.js
// ...
// import Repo
import Repo from './modules/Repo'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>
      <Route path="/repos" component={Repos}/>
      {/* 注意这里的路径 带了 ：参数 */}
      <Route path="/repos/:userName/:repoName" component={Repo}/>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))
```

接下来访问 /repos/reactjs/react-router 和 /repos/facebook/react 就会看到不同的内容了。

##六 默认路由

```
// index.js
import { Router, Route, hashHistory, IndexRoute } from 'react-router'
// and the Home component
import Home from './modules/Home'

// ...

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>

      {/* 注意这里* /}
      <IndexRoute component={Home}/>

      <Route path="/repos" component={Repos}>
        <Route path="/repos/:userName/:repoName" component={Repo}/>
      </Route>
      <Route path="/about" component={About}/>
    </Route>
  </Router>
), document.getElementById('app'))
```

这里添加了IndexRoute来指定默认的路径 / 所对应的组件。注意它没有path属性值。

同理也有 默认链接组件 IndexLink。、

##七 使用Browser History

前面的例子一直使用的是hashHistory，因为它一直可以运行，但更好的方式是使用Browser History，它可以不依赖哈希端口 （#）。

首先需要改 index.js:

```
// ...
// bring in `browserHistory` instead of `hashHistory`
import { Router, Route, browserHistory, IndexRoute } from 'react-router'

render((
{/* 注意这里 */}
  <Router history={browserHistory}>
    {/* ... */}
  </Router>
), document.getElementById('app'))
```

其次需要 修改webpack的本地服务配置，打开 package.json 添加 --history-api-fallback ：

```
"start": "webpack-dev-server --inline --content-base . --history-api-fallback"
```

最后需要在 index.html中 将文件的路径改为相对路径：

```
<!-- index.html -->
<!-- index.css 改为 /index.css -->
<link rel="stylesheet" href="/index.css">

<!-- bundle.js 改为 /bundle.js -->
<script src="/bundle.js"></script>
```

这样就去掉了url中的 # 。

## 三 资源与参考

### 1官网
英文官网
https://reacttraining.com/react-router/

github
https://github.com/ReactTraining/react-router

React Router中文官网
http://reacttraining.cn/

### 2文档
官方文档（web模块）：
https://reacttraining.com/react-router/web/guides/philosophy

React Router 中文文档
https://react-guide.github.io/react-router-cn/