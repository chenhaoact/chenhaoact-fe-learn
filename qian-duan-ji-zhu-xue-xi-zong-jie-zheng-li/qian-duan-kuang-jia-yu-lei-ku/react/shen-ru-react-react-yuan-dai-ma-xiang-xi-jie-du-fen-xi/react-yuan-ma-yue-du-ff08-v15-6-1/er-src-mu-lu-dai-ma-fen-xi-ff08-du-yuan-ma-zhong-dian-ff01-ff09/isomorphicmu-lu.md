isomorphic 是一个十分重要的目录，里边基本上放置了你**在React日常编程中常使用到的东西的定义,比如：React模块,React.Component等**：

![](/assets/WX20171009-194209@2x.png)

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

#### ReactElement.js

这里定义了ReactElement，用到了工厂模式，传入的参数中有我们非常熟悉的一些React元素的属性，如：key, ref，props等，下面还在ReactElement上挂载了一些方法，如：createElement，cloneElementd等：

![](/assets/WX20171004-185552@2x.png)

#### ReactChildren.js
这里定义了React元素的子元素模块和它的一些方法：

![](/assets/WX20171004-195809@2x.png)


