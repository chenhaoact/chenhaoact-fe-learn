# requestAnimationFrame
## 一 简介
**requestAnimationFrame是浏览器用于定时循环操作的一个接口**，类似于setTimeout，**主要用途是按帧对网页进行重绘**。

设置这个API的**目的是为了让各种网页动画效果（DOM动画、Canvas动画、SVG动画、WebGL动画）能够有一个统一的刷新机制，从而节省系统资源，提高系统性能**，改善视觉效果。代码中使用这个API，就是告诉浏览器希望执行一个动画，让浏览器在下一个动画帧安排一次网页重绘。

requestAnimationFrame的优势，在于充分利用显示器的刷新机制，比较节省系统资源。

## 二 使用
TODO

## 参考
### 已学习

### 待学习
[《JavaScript 标准参考教程（alpha）》，阮一峰 Web API - requestAnimationFrame](http://javascript.ruanyifeng.com/htmlapi/requestanimationframe.html)

[HTML5探秘：用requestAnimationFrame优化Web动画](http://www.webhek.com/post/requestanimationframe.html)

