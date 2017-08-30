# dom元素（Element）对象属性与方法整理

## 一 dom元素属性
### 1 特征相关属性
Element.attributes 返回一个类似数组的对象，成员是当前元素节点的所有属性节点

Element.id属性返回指定元素的id属性，该属性可读写。

Element.tagName 返回指定元素的大写标签名，与nodeName属性的值相等。

Element.innerHTML 返回该元素包含的 HTML 代码。该属性**可读写**，常用来设置某个节点的内容。

Element.outerHTML 返回一个字符串，内容为指定元素节点的所有HTML代码，**包括它自身和包含的所有子元素**。可读写。

Element.className 用来读写当前元素节点的class属性。它的值是一个字符串，每个class之间用空格分割。

Element.classList 返回一个类似数组的对象，当前元素节点的每个class就是这个对象的一个成员

### 2 盒模型相关属性
#### Element.clientHeight，Element.clientWidth
Element.clientHeight 返回元素节点可见部分的高度
Element.clientWidth 返回元素节点可见部分的宽度

不包括溢出（overflow）的大小，只返回该元素在容器中占据的大小。有滚动条的元素来说，它们等于滚动条围起来的区域大小。包括Padding、但不包括滚动条、边框和Margin，单位像素。

#### Element.scrollHeight，Element.scrollWidth
Element.scrollHeight 返回某个网页元素的总高度
Element.scrollWidth 返回总宽度

可理解成元素在**垂直和水平方向上可以滚动的距离**。包括由于溢出容器而无法显示在网页上的那部分高度或宽度。只读属性。

它们返回的是整个元素的高度或宽度，包括由于存在滚动条而不可见的部分。默认情况下，它们包括Padding，但不包括Border和Margin。


## 二 dom元素方法



##参考
### 已学习


### 待学习
Element对象（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/element.html

属性的操作（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/attribute.html

CSS操作（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/css.html









