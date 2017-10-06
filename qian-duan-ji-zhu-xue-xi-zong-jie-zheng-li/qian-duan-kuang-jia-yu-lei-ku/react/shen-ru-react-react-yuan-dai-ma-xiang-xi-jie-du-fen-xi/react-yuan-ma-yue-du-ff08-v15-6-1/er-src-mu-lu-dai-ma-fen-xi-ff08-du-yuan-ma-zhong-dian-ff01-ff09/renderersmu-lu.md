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

fiber下重写了React核心算法，架构进行了升级，未来可能会应用。

![](/assets/WX20171006-211013@2x.png)

#### dom/shared

dom/shared下放置了一些共用的DOM操作方法，如findDOMNode, setInnerHTML，CSSProperty, DOMProperty等：

![](/assets/WX20171006-212318@2x.png)


### 2. Native的渲染逻辑主要是在native目录下：

![](/assets/WX20171004-202405@2x.png)

可以看到这里有很多ReactNative开头的文件，这里和ReactNative有很多联系，以通过React跨平台实现Android和iOS开发。

### 3. shared目录
渲染逻辑的共享类，其他渲染目录都能公用到的一些工具函数都放置在此：

![](/assets/WX20171006-203127@2x.png)

需要注意的是这几个目录：

#### （1）shared/stack/reconciler

协调器，包含自定义组件实现ReactCompositeComponent.js， setState机制，生命周期方法流程，DOM diff等

![](/assets/WX20171006-213028@2x.png)

#### （2）shared/shared/event

这里定义了事件处理机制的一些方法：

![](/assets/WX20171006-213238@2x.png)

#### （3）shared/fiber

shared下也有fiber目录，是一些实验代码，未来可能会应用：

![](/assets/WX20171006-213704@2x.png)




























