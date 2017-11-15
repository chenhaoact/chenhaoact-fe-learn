# 浏览器原理

## 一 渲染原理
### 渲染六部曲
一个页面的呈现，粗略的说会经过以下这些步骤：

1. **DOM 树构建**
2. **构建 CSSOM 树（计算 Style）** 
3. **合并 DOM 树与 CSSOM 树为 Render 树**
4. **布局**（Layout）
5. **绘制**（Paint）
6. 复合图层化（Composite）

其中布局（Layout）环节主要负责各元素尺寸、位置的计算，绘制（Paint）环节则是绘制页面像素信息，合成（Composite）环节是多个复合层的合成，最终合成的页面被用户看到。

### 重排 reflow 与 重绘 repaint
1. 重排 reflow
当改变**影响到文本内容、结构或元素位置时，会发生**。

2. 重绘 repaint
改变不会影响元素的位置及大小的样式时，则会触发重绘。换句话说，**元素改变外观时会触发这个行为，不包括修改元素的几何属性**。

例如background,visibility。

##参考
### 待学习
浏览器渲染的那些事(一)
https://segmentfault.com/a/1190000005169412

浏览器渲染的那些事（二）
https://segmentfault.com/a/1190000005177695

浏览器渲染的那些事（三）
https://segmentfault.com/a/1190000005598925

浏览器内核、JS 引擎、页面呈现原理及其优化
https://www.zybuluo.com/yangfch3/note/671516