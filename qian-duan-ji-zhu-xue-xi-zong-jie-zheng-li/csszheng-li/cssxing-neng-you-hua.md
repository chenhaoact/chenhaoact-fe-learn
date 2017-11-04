# CSS性能优化

## CSS 优化主要是四个方面：
1. 加载性能（压缩等）

2. 选择器性能

3. 渲染性能（重点）
渲染性能是 CSS 优化最重要的关注对象。页面渲染 junky 过多？看看是不是大量使用了 text-shadow？是不是开了字体抗锯齿？CSS 动画怎么实现的？合理利用 GPU 加速了吗？用了 Flexible Box Model？有没有测试换个 layout 策略对 render performance 的影响？这个方面**搜索 CSS render performance 或者 CSS animation performance** 也会有一堆一堆的资料可供参考。


4. 可维护性、健壮性

详细参考：

CSS 优化、提高性能的方法有哪些？ -知乎
https://www.zhihu.com/question/19886806

