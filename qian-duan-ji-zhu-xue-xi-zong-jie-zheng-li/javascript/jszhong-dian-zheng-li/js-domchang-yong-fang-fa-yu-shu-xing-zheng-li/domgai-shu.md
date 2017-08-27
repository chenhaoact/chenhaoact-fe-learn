# dom概述

## 一 概念
**js 操作网页（html文档）的api, document是其顶级对象。**

## 二 作用
将网页转为一个JS对象，从而可以用脚本进行各种操作（如：增删改查网页内容）。

## 三 DOM标准
目前的通用版本是[DOM 3](https://www.w3.org/TR/2004/REC-DOM-Level-3-Core-20040407/core.html)，最新制定的版本是[DOM 4](https://www.w3.org/TR/dom/) （2015年已成为最新的dom标准）

## 四 DOM树
浏览器会根据DOM模型，将结构化文档（比如HTML和XML）**解析成一系列的节点，再由这些节点组成一个树状结构（DOM Tree）**。

最顶层的节点是document节点。它构成树结构的根节点（root node），其他HTML标签节点都是它的下级。

除根节点外，**其他节点都存在三种关系**：

父节点关系（parentNode）：直接的上级节点
子节点关系（childNodes）：直接的下级节点
**同级节点关系（sibling）**：拥有同一父节点

DOM提供
子节点接口（属性）：
firstChild（第一个子节点）
lastChild（最后一个子节点）

同级节点接口（属性）：
nextSibling（紧邻在后的同级节点）previousSibling（紧邻在前的同级节点）

## 五 节点（node）
DOM的最小组成单位叫做节点（node）。

**文档的树形结构（DOM树），是由各种不同类型的节点组成。**

**所有节点对象都是浏览器内置的Node对象的实例**，继承了Node的属性和方法。

### 1 节点的类型(七种)

Document：整个文档树的顶层节点
DocumentType：doctype标签（如<!DOCTYPE html>）
Element：各种HTML标签（如`<body>、<a>`）
Attribute：网页元素的属性（如class="right"）
Text：标签的文本
Comment：注释
DocumentFragment：文档的片段

### 2 Node（节点）对象的属性：
.nodeName 返回节点的名称
.nodeType 返回节点类型的常数值
.nodeValue 返回当前节点本身的文本值，该属性可读写
.textContent 返回当前节点和它的所有后代节点的文本内容
.baseURI 返回当前网页的绝对路径,该属性的值一般由当前网址的URL（即window.location属性）决定，但是可使用HTML的`<base>`标签，改变该属性的值

.nextSibling 返回紧跟在当前节点后面的第一个同级节点
.previousSibling 返回当前节点前面的、距离最近的一个同级节点
.parentNode 返回当前节点的父节点(可能是三种类型：element节点、document节点和documentfragment节点)
.parentElement 返回当前节点的父Element节点
.childNodes 返回一个NodeList集合，成员包括当前节点的所有子节点
.firstChild 返回当前节点的第一个子节点
.lastChild 返回当前节点的最后一个子节点

### 3 Node（节点）对象的方法（重点！）：
.appendChild() 接受一个节点对象作为参数，将其作为最后一个子节点，插入当前节点
.hasChildNodes() 返回一个布尔值，表示当前节点是否有子节点
.cloneNode() 克隆一个节点。它接受一个布尔值作为参数，表示是否同时克隆子节点，默认false，即不克隆子节点。克隆一个节点，会拷贝该节点的所有属性，但是会丧失addEventListener方法和on-属性（如node.onclick = fn），添加在这个节点上的事件回调函数。
.insertBefore() 将某节点插入当前节点的指定位置。第一个参数是所要插入的节点，第二个参数是当前节点的一个子节点，新的节点将插在这个节点的前面。该方法返回被插入的新节点。
.removeChild() 接受一个子节点作为参数，用于从当前节点移除该子节点。返回被移除的子节点。
.replaceChild 用于将一个新节点，替换当前节点的某一个子节点。接受两参数，第一个参数是用来替换的新节点，第二个参数将要被替换走的子节点。返回被替换走的那个节点。
.contains() 接受一个节点作为参数，返回布尔值，表示参数节点是否为当前节点的后代节点。
.isEqualNode() 返回一个布尔值，用于检查两个节点是否相等。所谓相等的节点，指两个节点的类型相同、属性相同、子节点相同
.normalize() 用于清理当前节点内部的所有Text节点。会去除空的文本节点，并且将毗邻的文本节点合并成一个。

## 六 NodeList 和 HTMLCollection

节点都是单个对象，有时**需要一种数据结构，能容纳多个节点。DOM提供两种集合对象，用于实现这种节点的集合：NodeList和HTMLCollection**。

许多DOM属性和方法，返回的结果是NodeList实例或HTMLCollection实例。

### 1 NodeList对象
NodeList实例对象是一个类似数组的对象，它的成员是节点对象。
如：document.querySelectorAll()返回的就是NodeList实例对象。

#### （1）NodeList实例对象是类数组结构但不是数组，不能**直接**使用js数组的方法

注意：
NodeList实例对象**提供length属性和数字索引**，因此可像数组那样，使用数字索引取出每个节点，但**它本身并不是数组，不能使用pop或push之类数组特有的方法**。

如果要在NodeList实例对象使用数组方法，可将NodeList实例转为真正的数组。另一种方法是通过call方法，间接在NodeList实例上使用数组方法。

#### （2）NodeList的遍历
遍历NodeList实例对象的首选方法，是**使用for循环**。

**不要使用for...in**循环去遍历NodeList实例对象，因为for...in循环会将非数字索引的length属性和下面要讲到的item方法，也遍历进去，而且不保证各个成员遍历的顺序。

ES6新增的**for...of循环，也可以**正确遍历NodeList实例对象。

### 2 HTMLCollection对象
HTMLCollection实例对象与NodeList实例对象类似，也是节点的集合，返回一个类似数组的对象。

如：document.links、docuement.forms、document.images等属性，返回的都是HTMLCollection实例对象。

#### （1）HTMLCollection与NodeList的区别：

（1）HTMLCollection实例对象的成员只能是Element节点，NodeList实例对象的成员可以包含其他节点。

（2）HTMLCollection实例对象都是动态集合，节点的变化会实时反映在集合中。NodeList实例对象可以是静态集合。

（3）HTMLCollection实例对象可以用id属性或name属性引用节点元素，NodeList只能使用数字索引引用。


##参考
### 已学习
DOM 模型概述（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/node.html














