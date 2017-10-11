# flex 布局
## 一 简介

**布局的传统解决方案，基于盒状模型，依赖 display 属性 + position属性 + float属性，对于那些特殊布局非常不方便**，比如，垂直居中就不容易实现。

09年，W3C 提出了一种新的方案----Flex 布局，**可以简便、完整、响应式地实现各种页面布局**。目前，它已经得到了所有浏览器的支持。

**Flex 布局将成为未来布局的首选方案。**

任何一个容器都可指定为 Flex 布局。

```
.box{
  display: flex;
}
```


行内元素也可使用 Flex 布局。

```
.box{
  display: inline-flex;
}
```

设为 Flex 后，子元素的float、clear和vertical-align失效。


采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

## 二 flex 容器常用属性

### 1. flex-direction
flex-direction属性决定主轴的方向（即项目的排列方向）。

```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```


### 2. flex-wrap 如何换行排布
flex-wrap：nowrap | wrap | wrap-reverse
默认值：nowrap

nowrap：
flex容器为单行。该情况下flex子项可能会溢出容器
wrap：
flex容器为多行。该情况下flex子项溢出的部分会被放置到新行，子项内部会发生断行
wrap-reverse：
反转 wrap 排列。

### 3. flex-flow
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

```
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

### 4. justify-content
justify-content属性定义了项目在主轴上的对齐方式。


```

.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

可取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### 5. align-items

align-items属性定义项目在交叉轴上如何对齐。


```
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

可取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。


### 6. align-content
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

```
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

## 三 flex （容器里）项目的常用属性
### 1. flex
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}

```

该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

比如：
**一个flex容器中只有一个元素，为其指定flex:1,则该元素占满容器剩余空间。**

### 2. order
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```
.item {
  order: <integer>;
}
```

### 3. flex-grow（重要）
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。**如果定义为1则占满所有的剩余空间。（可用来做响应式适配，分配满剩余空间）**

```
.item {
  flex-grow: <number>; /* default 0 */
}
```
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### 4. flex-shrink
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。负值对该属性无效。

```
.item {
  flex-shrink: <number>; /* default 1 */
}
```

### 5. flex-basis
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。


```
.item {
  flex-basis: <length> | auto; /* default auto */
}
```
它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

### 6. align-self
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

```
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

## 四 资源与参考

### 1教程
#### （1）已学习：

[Flex 布局教程：语法篇（阮一峰）](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

#### （2）学习中：

#### （3）待学习：
[Flex 布局教程：实例篇（阮一峰）](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

[flex-wrap - CSS3参考手册](http://www.css88.com/book/css/properties/flex/flex-wrap.htm)