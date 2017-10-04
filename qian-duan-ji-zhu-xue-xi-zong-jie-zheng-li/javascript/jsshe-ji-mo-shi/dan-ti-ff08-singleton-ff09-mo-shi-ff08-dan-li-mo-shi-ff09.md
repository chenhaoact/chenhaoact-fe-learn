（1）**单体（Singleton）模式（单例模式）**： 绝对是JavaScript中最基本最有用的模式。

单例概念：保证一个类只有一个实例

实现的方法：先判断实例存在与否，存在直接返回，不存在就创建了再返回，这确保一个类只有一个实例对象。

用途：
a.用来划分命名空间，从全局命名空间里提供一个唯一的访问点来访问该对象。
b.实现模块内部保护，模块之间通信
　　
优点：可以减少网页中全局变量的数量(在网页中使用全局变量有风险)；可以在多人开发时避免代码的冲突(使用合理的命名空间)等。

使用注意事项：

a.this的使用
b.闭包容易造成内存泄漏，不需要赶快处理掉
c.注意new的成本（继承）

实例：

```javascript
<script>
    //top模块(与下面的banner模块是独立的命名空间,互不干扰(自己保护自己),相互可以通信)
    var top = {
        init: function () {
            //先绑定dom元素
            this.render();
            //再为dom元素绑定事件
            this.bind();
        },
        a: 4, //想传递的量
        //render 把所有的dom元素放在这里边
        render: function () {
            var me = this;
            me.btn_a = $('#a');
        },
        //bind 给元素绑定事件
        bind: function(){
            var me = this;
            me.btn_a.click(function(){
                //业务逻辑,定义在下边
                me.test();
            });
        },
        test: function(){
            a = 5;
        }

    };


    //banner模块
    var banner = {
        init: function () {
            //先绑定dom元素
            this.render();
            //再为dom元素绑定事件
            this.bind();
        },
        a: 4, //想传递的量
        //render 把所有的dom元素放在这里边
        render: function () {
            var me = this;
            me.btn_a = $('#a');
        },
        //bind 给元素绑定事件
        bind: function(){
            var me = this;
            me.btn_a.click(function(){
                //业务逻辑,定义在下边
                me.test();
            });
        },
        test: function(){
            //a = 6;
            top.a = 6;//直接调用模块 top. ... 实现和top的通信
        }
    };

    //初始化各模块
    top.init();
    banner.init();
    
</script>
```

详细请参考：http://www.cnblogs.com/TomXu/archive/2012/02/20/2352817.html

