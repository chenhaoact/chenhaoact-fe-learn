### Context

有时，**若想不通过在每一级组件设置prop的方式来向组件树内传递数据。那么，React的"context"特性可以做到**这点。

大多数应用将不会需要用到context。尤其是刚开始用React。**使用context将会使你的代码难以理解，因为它让数据流变得不清晰。它类似于在你的应用里用以传递state的全局变量。**

如果必须使用context，请保守使用。

不论创建一个应用或者是库，试着缩小context的使用范围，并尽可能避免直接使用context相关API，以便在API变动时容易升级。

具体使用参考：  
[https://facebook.github.io/react/docs/context.html](https://facebook.github.io/react/docs/context.html)

