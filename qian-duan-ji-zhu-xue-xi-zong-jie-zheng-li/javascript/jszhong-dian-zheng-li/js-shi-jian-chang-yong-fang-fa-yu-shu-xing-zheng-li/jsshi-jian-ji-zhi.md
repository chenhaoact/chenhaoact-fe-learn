# js事件机制与事件模型

## 一 DOM事件流三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段。

### 1. 事件捕获：
当鼠标点击或者触发dom事件时，浏览器**从根节点开始由外到内进行事件传播**，即点击子元素，如父元素通过事件捕获方式注册对应事件，会先触发父元素绑定的事件。

### 2. 处于目标阶段：

### 3. 事件冒泡：
事件冒泡顺序是**由内到外**进行事件传播，**直到根节点**。

### dom标准事件流的触发先后顺序为：先捕获再冒泡

## 二 addEventListener

```
addEventListener
(event, listener, useCapture)　　
```

参数定义：
event---（事件名称，如click，不带on），listener---事件监听函数，
useCapture---是否采用事件捕获进行事件捕捉，默认为false，即采用事件冒泡方式


### 事件触发器 dispatchEvent

```
// 触发事件
var event = new Event('click');
document.dispatchEvent(event);
```



## 三 例子
###默认的事件冒泡例子：


```
<body>
    <div id="parent">
        父元素
        <div id="child">
            子元素
        </div>
    </div>
    <script type="text/javascript">
        var parent = document.getElementById("parent");
        var child = document.getElementById("child");
    
        document.body.addEventListener("click",function(e){
            console.log("click-body");
        },false);
        
        parent.addEventListener("click",function(e){
            console.log("click-parent");
        },false);

        child.addEventListener("click",function(e){
            console.log("click-child");
        },false);
    </script>
</body>
```

输出的顺序：
click-child 
click-parent 
click-body

**默认addEventListener注册的事件触发顺序是由内到外的，这就是事件冒泡**。

#### 点击**子元素不想触发父元素的事件**怎么办？用**停止事件传播event.stopPropagation()**



```
child.addEventListener("click",function(e){
　　console.log("click-child");
  　e.stopPropagation();  //注意这行！！！
},false);
```

在点击子元素的时候就只弹出了子元素那条信息，父元素的事件没有触发，因为事件已经停止传播了，冒泡阶段也就停止了。


### 事件捕获例子

修改栗子1中的代码，给parent元素注册一个捕获事件，如下


```
　　　　 var parent = document.getElementById("parent");
        var child = document.getElementById("child");
    
        document.body.addEventListener("click",function(e){
            console.log("click-body");
        },false);
        
        parent.addEventListener("click",function(e){
            console.log("click-parent---事件传播");
        },false);
　　　　 
　　　　 //新增事件捕获事件代码（把addEventListener第三个参数设置为true）
        parent.addEventListener("click",function(e){
            console.log("click-parent--事件捕获");
        },true);

        child.addEventListener("click",function(e){
            console.log("click-child");
        },false);
```

输出的顺序：
click-parent （事件捕获阶段就触发一次）
click-child 
click-parent （事件冒泡阶段也用addEventListener注册了一个事件，所以也触发一次）
click-body

## 四 事件委托（事件代理）
**当需要对很多元素添加事件时，可通过将事件添加到它们的父节点**而将事件委托给父节点来触发处理函数。（而非通过循环或穷举一个一个去给每一个元素添加事件）这**得益于浏览器的事件冒泡机制**，

即可以通过js原生的addEventListener实现，也可以用jQuery 中的$.on() 或 $.on某具体事件() 实现:

如：


```
var parent = document.getElementById("parent");
var child = document.getElementById("child");
//注意下面    
parent.onclick = function(e){
            if(e.target.id == "child"){
                console.log("您点击了child元素")
            }
}
```

虽然没有直接只child元素注册click事件，可是点击child元素时却弹出了提示信息。

## removeEventListener()
removeEventListener方法用来移除addEventListener方法添加的事件监听函数。

```
div.addEventListener('click', listener, false);
div.removeEventListener('click', listener, false);

```

removeEventListener方法的参数，与addEventListener方法完全一致。它的第一个参数“事件类型”，大小写敏感。

注意，removeEventListener方法移除的监听函数，必须与对应的addEventListener方法的参数完全一致，而且必须在同一个元素节点，否则无效。



##参考
### 已学习
JavaScript 详说事件机制之冒泡、捕获、传播、委托
http://www.cnblogs.com/bfgis/p/5460191.html

### 待学习
事件模型（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/event.html

w3c dom事件规范  
[https://www.w3.org/TR/DOM-Level-3-Events/](https://www.w3.org/TR/DOM-Level-3-Events/)










