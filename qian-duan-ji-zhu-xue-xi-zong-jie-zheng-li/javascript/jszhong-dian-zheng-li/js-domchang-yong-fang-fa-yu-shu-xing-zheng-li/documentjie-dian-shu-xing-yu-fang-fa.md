# document属性与方法

## 一 document属性
### 1 节点属性

#### （1）document.doctype
当前文档类型（Document Type Declaration，简写DTD）。HTML5文档为`<!DOCTYPE html>`

#### （2）document.body，document.head
document.head 返回当前文档的`<head>`节点
document.body 返回当前文档的`<body>`

### 2 节点集合属性
这些属性返回文档内特定元素的集合。这些集合是动态的，原节点有任何变化，立刻反映在集合中。

#### （1）document.links，document.forms，document.images，document.embeds
document.links 返回文档所有设定了href属性的a及area元素

document.forms 返回页面中所有表单元素

document.images 返回页面所有图片元素

document.embeds 返回网页中所有嵌入对象，即embed标签

#### （2）document.scripts，document.styleSheets

### 3 文档信息属性
#### （1）document.documentURI
当前文档的网址。

#### （2）document.domain
当前文档的域名

#### (3)document.characterSet
返回渲染当前文档的字符集，如UTF-8、ISO-8859-1。

####（4）document.readyState
返回当前文档的状态，共有三种值：

loading：加载HTML代码阶段（尚未完成解析）
interactive：加载外部资源阶段时
complete：加载完成时

####（5）document.cookie
用来操作浏览器Cookie

## 二 document方法
### 1 查找节点的方法（重点）
#### （1）document.querySelector()，document.querySelectorAll()

document.querySelector() 接受CSS选择器为参数，返回匹配该选择器的元素节点。如有多个节点满足，则返第一个匹配的节点

**document.querySelectorAll() **与querySelector用法类似，区别是返回一个NodeList对象，**包含所有匹配给定选择器的节点**。

#### (2)document.getElementsByTagName()
document.getElementsByTagName() 返回**所有**指定HTML标签的元素，返回值是一个类似数组的HTMLCollection对象，可实时反映HTML文档的变化

####  (3)document.getElementsByClassName()
document.getElementsByClassName() 返回一个类数组的对象（HTMLCollection实例对象），包括了所有**class名字符合指定条件的元素**，元素的变化实时反映在返回结果中。

注意：由于class是保留字，所以JS一律使用className表示CSS的class。

#### （4）document.getElementsByName()
选择拥有name属性的HTML元素，返回一个类似数组的的对象（NodeList对象的实例），因为name属性相同的元素可能不止一个

#### (5)document.getElementById()
返回匹配指定id属性的元素节点

#### (6)document.elementFromPoint()
返回位于页面指定位置最上层的那个HTML元素。

### 2 生成节点的方法
#### （1）document.createElement()
生成网页元素节点

参数为元素的标签名，即元素节点的tagName属性（如div或a）

### 3 



##参考
### 已学习
document节点（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/document.html

### 待学习








