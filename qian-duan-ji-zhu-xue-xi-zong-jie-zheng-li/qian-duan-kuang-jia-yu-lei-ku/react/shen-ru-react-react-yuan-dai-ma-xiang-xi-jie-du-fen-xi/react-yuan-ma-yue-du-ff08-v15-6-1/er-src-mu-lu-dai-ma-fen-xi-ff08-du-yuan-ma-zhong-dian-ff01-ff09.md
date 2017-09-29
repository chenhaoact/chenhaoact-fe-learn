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
isomorphic 是一个十分重要的目录，里边基本上放置了你**在React日常编程中常使用到的东西的定义,比如：React模块,React.Component等**：

![](/assets/WX20170810-141121@2x.png)

先从src/isomorphic/目录最外层的ReactEntry.js开始看：

#### ReactEntry.js （顾名思义，这是React的入口，定义React模块的地方）

![](/assets/WX20170929-194323@2x.png)

![](/assets/WX20170929-194836@2x.png)

这里定义了React这个对象，它有Children,Component,PureComponent,createElement等一系列的属性，最终将React这个对象导出为全局的React模块。

这些属性又分别定义在isomorphic下的 children/ReactChildren.js，classic/element/ReactElement.js,modern/class/ReactBaseClasses.js等文件中：

![](/assets/WX20170929-195306@2x.png)


#### ReactBaseClasses.js
在用ES2015写组件时 class Hello extends **React.Component 是在(src/isomorphic/modern/class/ReactBaseClasses.js)这里定义**:

![](/assets/reactcomponentdifine.png)

这里也在**ReactComponet的原型对象上定义了一些方法，比如我们经常用到的setState**:

![](/assets/reactsetstatefuncdef.png)

**ReactBaseClasses.js（定义React中一些最基本的类）**中除了React.Component，还定义了PureComponent和AsyncComponent：

![](/assets/WX20170929-193020@2x.png)




### 5. shared目录
![](/assets/WX20170810-141424@2x.png)

### 6. test目录
![](/assets/WX20170810-141450@2x.png)

### 7. renderers目录

![](/assets/WX20170810-142543@2x.png)






























