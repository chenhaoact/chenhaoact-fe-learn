## 二 src目录代码分析（读源码重点！）

**回到源码src目录:**

renderers 顾名思义这是关于如何渲染的逻辑都放置在这里，有两个版本分别是浏览器和Native。shared 属于共享类，大家都能用到的一些工具函数都放置在此。那么 addons 呢？ 从源码中能看到比如做简单动画时用到的 ReactCSSTransitionGroup 都放置在此。

### 1. ReactVersion.js

此文件定义React的版本，如：

![](/assets/asdfasfavavfava.png)

### 2. __mocks__目录
![](/assets/WX20170810-1668727@2x.png)

### 3. fb目录

#### (1) ReactDOMFiberFBEntry.js

![](/assets/WX20170810-140838@2x.png)


### 4. isomorphic目录
isomorphic 目录基本上放置了你**在日常编程中能使用到的东西**：

![](/assets/WX20170810-141121@2x.png)

如： ReactComponet ，在用ES2015写组件时 class Hello extends **React.Component 就是在(src/isomorphic/modern/class/ReactBaseClasses.js)这里定义**:

![](/assets/reactcomponentdifine.png)

这里也在**ReactComponet的原型对象上定义了一些方法，比如我们经常用到的setState**:

![](/assets/reactsetstatefuncdef.png)


### 5. shared目录
![](/assets/WX20170810-141424@2x.png)

### 6. test目录
![](/assets/WX20170810-141450@2x.png)

### 7. renderers目录

![](/assets/WX20170810-142543@2x.png)






























