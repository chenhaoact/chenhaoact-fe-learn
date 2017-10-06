renderers 目录实现了如何渲染的逻辑，是React的核心之一，有两个版本分别是浏览器和Native：

![](/assets/WX20171004-202112@2x.png)

### 1. 浏览器的渲染逻辑比较重要在dom目录

![](/assets/WX20171004-202254@2x.png)

可以看到dom下除了测试的test和共用方法的shared外，主要分了stack（分为client
和server）和fiber两个目录：

#### (1) dom/stack/client

这里定义了各种ReactComponent：

![](/assets/WX20171006-210252@2x.png)

#### (2) dom/stack/server

这里定义了服务端渲染的相关方法：

![](/assets/WX20171006-210359@2x.png)

#### dom/fiber



### 2. Native的渲染逻辑主要是在native目录下：

![](/assets/WX20171004-202405@2x.png)

可以看到这里有很多ReactNative开头的文件。

### 3. shared目录
属于共享类，其他渲染目录都能公用到的一些工具函数都放置在此：

![](/assets/WX20171006-203127@2x.png)



























