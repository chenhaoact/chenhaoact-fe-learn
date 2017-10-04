概念：**定义一个用于创建对象的接口**，该接口**由子类决定实例化哪一个类**。该模式使一个类的实例化延迟到了子类。而子类可以重写接口方法以便创建的时候指定自己的对象类型。

**用途：**

适用于：
a.对象的构建较复杂时的场景
b.需要依赖具体的环境创建不同实例。
c.处理大量具有相同属性的小对象。

注意事项：
a.不要滥用工厂模式，如果只是为了生产很好的几个对象，创建工厂只会增加代码复杂度。（会生产大量小对象才适合建工厂流水线）

优点：**消除对象之间的耦合**(何为耦合？就是相互影响)。通过使用工厂方法而不是new关键字及具体类，可以把所有实例化的代码都集中在一个位置，**有助于创建模块化的代码**

```javascript
<script>
    //工厂是一个单体(单例模块)
    var myFactory = {};

    //不同的工厂流水线
    myFactory.product_shoes = function(){
        this.workers = 100;
        alert('生产鞋子');
    };
    myFactory.product_clothes = function(){
        this.workers = 500;
        alert('生产衣服');
    };
    //定义一个类,它的实例化延迟到了下面的子类里
    myFactory.manager = function(para){
        return new myFactory[para]();
    }
    //子类,进行实例化,决定生产哪种和哪样的东西
    var somebody = myFactory.manager('product_shoes');
    //alert(somebody.workers);

</script>
```

另一个非常有名的一个示例 - XHR工厂：

```javascript
var XMLHttpFactory =function(){};　　　　　　//这是一个简单工厂模式
　　XMLHttpFactory.createXMLHttp =function(){
　　　 var XMLHttp = null;
　　　　if (window.XMLHttpRequest){
　　　　　　XMLHttp = new XMLHttpRequest()
　　　 }elseif (window.ActiveXObject){
　　　　　　XMLHttp = new ActiveXObject("Microsoft.XMLHTTP")
　　　　}
　　return XMLHttp;
　　}
　　//XMLHttpFactory.createXMLHttp()这个方法根据当前环境的具体情况返回一个XHR对象。
　　var AjaxHander =function(){
　　　　var XMLHttp = XMLHttpFactory.createXMLHttp();
　　　　...
　　}
```

工厂有简单工厂，抽象工厂之分:

```
var XMLHttpFactory =function(){};　     //这是一个抽象工厂模式
　　XMLHttpFactory.prototype = {
   　　//如果真的要调用这个方法会抛出一个错误，它不能被实例化，只能用来派生子类
   　　createFactory:function(){
      　　thrownew Error('This is an abstract class');
   　　}
　　}
　　//派生子类，文章开始处有基础介绍那有讲解继承的模式，不明白可以去参考原理
　　var XHRHandler =function(){
   　　XMLHttpFactory.call(this);
　　};
　　XHRHandler.prototype =new XMLHttpFactory();
　　XHRHandler.prototype.constructor = XHRHandler;
　　//重新定义createFactory 方法
　　XHRHandler.prototype.createFactory =function(){
   　　var XMLHttp =null;
   　　if (window.XMLHttpRequest){
      　　XMLHttp =new XMLHttpRequest()
   　　}elseif (window.ActiveXObject){
      　　XMLHttp =new ActiveXObject("Microsoft.XMLHTTP")
   　　}
   　　return XMLHttp;
　　}
```

**区别：**
简单工厂 ： 用来生产同一等级结构中的任意产品。（对于**增加新的产品，无能为力**）
工厂方法 ：用来生产同一等级结构中的固定产品。（支持增加任意产品）   
抽象工厂 ：用来生产不同产品族的全部产品。（对于增加新的产品，无能为力；**支持增加产品族**）  
 
以上三种工厂 方法在等级结构和产品族这两个方向上的支持程度不同。所以要根据情况考虑应该使用哪种方法。  
 
简单工厂优点：客户端可以免除直接创建产品对象的责任，而仅仅是“消费”产品。简单工厂模式通过这种做法实现了对责任的分割。
工厂方法有点：允许系统在不修改具体工厂角色的情况下引进新产品。 
抽象工厂优点：向客户端提供一个接口，使得客户端在不必指定产品具体类型的情况下，创建多个产品族中的产品对象 

抽象工厂简单工厂等的更详细区别请见：http://zyjustin9.iteye.com/blog/2094960

