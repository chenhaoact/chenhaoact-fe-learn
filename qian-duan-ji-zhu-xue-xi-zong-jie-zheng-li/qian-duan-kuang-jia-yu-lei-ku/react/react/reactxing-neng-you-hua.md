###react性能优化


react性能优化的重中之重是**减少渲染次数**，为了达到这个目的，一方面，需要合理拆分组件，有效地隔离组件之间的相互干扰；另一方面，要**减少组件的多余渲染**，减少不必要的操作和dom渲染。

1）根据业务逻辑划分组件时，可以考虑每个组件的本身特性，合理选择组件拆分的粒度、恰当使用纯组件。
2）**减少组件的多余渲染，归根结底就是shouldComponentUpdate的优化**，一方面可以依据状态的变化情况，拦截多余的渲染；另一方面**可以通过一些工具，比如redux / pure / onlyUpdateForKeys / shouldUpdate / shadowEqual / Immutable等，降低shouldComponentUpdate比较的成本**;
3) 养成良好的编程风格，减少由于变量变化，导致的多余渲染。


TODO

[https://facebook.github.io/react/docs/optimizing-performance.html](https://facebook.github.io/react/docs/optimizing-performance.html)

