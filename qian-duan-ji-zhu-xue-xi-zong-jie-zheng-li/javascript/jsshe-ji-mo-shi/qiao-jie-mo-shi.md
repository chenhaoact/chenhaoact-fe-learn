概念：将抽象部分与它的实现部分分离，使它们都可以独立地变化。

用途：最常用在事件监控上。在实现API的时候，桥接模式非常有用。在所有模式中，这种模式最容易立即付诸实施。

优点：可以用来弱化它与使用它的类和对象之间的耦合，就是将抽象与其实现隔离开来，以便二者独立变化；这种模式对于JavaScript中常见的时间驱动的编程有很大益处。桥接模式让API更加健壮，提高组件的模块化程度，促成更简洁的实现，并提高抽象的灵活性。

```javascript
//错误的方式
　　//这个API根据事件监听器回调函数的工作机制，事件对象被作为参数传递给这个函数。本例中并没有使用这个参数，而只是从this对象获取ID。
　　addEvent(element,'click',getBeerById);
　　function(e){
   　　var id =this.id;
   　　asyncRequest('GET','beer.url?id='+ id,function(resp){
      　　//Callback response
     　　 console.log('Requested Beer: '+ resp.responseText);
   　　});
　　}

　　//好的方式
　　//从逻辑上分析，把id传给getBeerById函数式合情理的，且回应结果总是通过一个回调函数返回。这么理解，我们现在做的是针对接口而不是实现进行编程，用桥梁模式把抽象隔离开来。
　　function getBeerById(id,callback){
   　　asyncRequest('GET','beer.url?id='+ id,function(resp){
      　　callback(resp.responseText)
   　　});
　　}
　　addEvent(element,'click',getBeerByIdBridge);
　　function getBeerByIdBridge(e){
   　　getBeerById(this.id,function(beer){
      　　console.log('Requested Beer: '+ beer);
   　　});
　　}
```

