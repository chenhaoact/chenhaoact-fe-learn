# 组件间的通信

## 一 父类更新子类（父组件传递数据给子组件）
父组件把 state的数据 传递给 子组件的props 
(任何state的改变都会触发子组件的componenetWillUpdate())



```js
class Children extends React.Component{
  render(){
    return (<div>
      {this.props.parentAttr}
    </div>);
  }
}

class Parent extends React.Component{
  render(){
    return (<Children parentAttr={this.state.attr}>
    </Children>);
  }
}
```

## 二 子类更新父类（子组件传递数据给父组件，通过回调函数）

```js
<Child someCallback={this.parentCallBackFunc.bind(this)}>
```

子组件中通过this.props.someCallback 拿到父组件的函数，可以去执行父组件中定义的函数对父组件数据进行一些操作。

## 三 兄弟组件间通信

当**两个组件不是父子关系，但有相同的父组件时，将这两个组件称为兄弟组件**。兄弟组件不能直接相互传送数据，此时可以**将数据挂载在父组件中**，由两个组件共享：如果组件需要数据渲染，则由父组件通过props传递给该组件；如果组件需要改变数据，则父组件传递一个改变数据的回调函数给该组件，并在对应事件中调用。

参考：
[ReactJS组件见沟通的一些方法
](http://www.alloyteam.com/2016/01/some-methods-of-reactjs-communication-between-components/)

## refs

ref可以被看作是一个组件的参考，也可以说是一个标识。作为组件的属性，其属性值可以是一个字符串也可以是一个函数。

有几个场景使用这种方式是有益的：查找渲染出的组件的DOM标记（可以认为是DOM的标识ID），在一个大型的非React应用中使用React组件或者是将你现有的代码转化成React。

下面的例子经常被用于ref的讲解，可见下面描述的场景应该是比较经典的）：通过某个事件使`<input />`元素的值被设为空字符串，然后使该`<input />`元素获得焦点。


ref加字符串作为属性：

React支持一个特殊的属性，你可以将这个属性加在任何通过render()返回的组件中。这也就是说对render()返回的组件进行一个标记，可以方便的定位的这个组件实例。这就是ref的作用。

ref的形式如下

```
<input ref="myInput" />
```

**要想访问这个实例，可以通过this.refs来访问：
**

```
this.refs.myInput

```

先前版本中，我们可以通过React.findDOMNode(this.refs.myInput)**来访问组件的DOM**。但现在，已经放弃了findDOMNode函数了，**可以直接使用this.refs.myInput来进行访问**。

参考：
[React组件refs详解](http://www.onmpw.com/tm/xwzj/web_154.html)

