#组件的继承扩展与多态

## 组件继承基础 (用extends ，然后在新组件内重写或添加扩展方法)


```
import A from '../components/a';

class B extends A {

constructor(props) {
    super(props);  
}  

//重写或者添加新的逻辑
renderHead() {    
return (...);  
}

render() {    
return (<div> 
...
{this.renderHead()}         
 </div>);  
}

}

export default B;

```

##

