### 1. 箭头函数和普通函数的区别 （面试常考） {#箭头函数和普通函数的区别}

1. **不绑定this**  
   箭头函数出现之前，每个新定义的函数都有其自己的 this 值。  
   **箭头函数会捕获其所在上下文的 this 值，作为自己的 this 值**

2. 通过 call\(\) 或 apply\(\) 方法调用一个函数时，只是传入了参数而已，对 this 并没有什么影响

3. 箭头函数不能用作构造器，和 new 一起用会抛出错误

4. **没有原型属性 .prototype**

5. 箭头函数当方法使用的时候没有定义this绑定

具体参考：  
[http://www.jianshu.com/p/eca50cc933b7](http://www.jianshu.com/p/eca50cc933b7)

[http://hughdai.github.io/2017/03/25/箭头函数与普通函数的区别/](http://hughdai.github.io/2017/03/25/箭头函数与普通函数的区别/)

