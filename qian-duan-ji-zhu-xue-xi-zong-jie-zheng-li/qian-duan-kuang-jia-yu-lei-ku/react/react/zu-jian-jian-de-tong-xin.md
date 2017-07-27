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





