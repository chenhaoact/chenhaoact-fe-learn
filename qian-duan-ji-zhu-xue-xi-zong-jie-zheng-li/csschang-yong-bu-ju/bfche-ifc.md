# BFC和IFC
## 一 简介 
### （1）IFC（行内格式化上下文）

#### 布局规则：
在IFC中，框(boxes)**一个接一个地水平排列**，起点是包含块的顶部。水平方向的 margin，border 和 padding在框之间得到保留。**框在垂直方向上可以以不同的方式对齐：顶部或底部对齐，或根据其中文字的基线对齐**。包含那些框的长方形区域，会形成一行，叫做行框。

#### 形成条件（满足其一即可）
只在**一个块级元素中仅包含内联元素**时才生成。

#### IFC用途






### （2）BFC（块级格式化上下文）
#### 布局规则：
1. 内部的Box会在**垂直方向一个接一个放置**。
2. Box**垂直方向的距离由margin决定**。属于同一个BFC的两个相邻Box的margin**会发生重叠**
3. 每个元素的左外边缘（margin-left)， 与包含块的左边（contain box left）相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。除非这个元素自己形成了一个新的BFC。
4. BFC的区域不会与float box重叠。
5. **BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此**。
6. **计算BFC的高度时，浮动元素也参与**计算

#### 形成条件（满足其一即可）
1. 根元素或其它包含它的元素
2. 浮动 (元素的 float 不是 none)
3. 绝对定位的元素 (元素具有 position 为 absolute 或 fixed)
4. 非块级元素具有 display: inline-block，table-cell, table-caption, flex, inline-flex
5. 块级元素具有overflow ，且值不是 visible或unset

#### BFC用途
1. 清除浮动



```
<div class="wrap">
<section>1</section>
<section>2</section>
</div>
```



```
.wrap {
  border: 2px solid yellow;
  width: 250px;
}
section {
  background-color: pink;
  float: left;
  width: 100px;
  height: 100px;
}
```


由于子元素都是浮动的，受浮动影响，边框为黄色的父元素的高度会塌陷：
![](/assets/2361702128-5925a4a7273c5_articlex.png)

解决方案：为 **.wrap 加上 overflow: hidden;**使其形成BFC，根据BFC规则第六条，**计算高度时就会计算float的元素的高度，达到清除浮动影响**的效果：

![](/assets/3996526225-5925a4c6649af_articlex.png)

2. 布局：**自适应两栏布局（重要）**



```
<div>
<aside></aside>
<main>我是好多好多文字会换行的那种蛤蛤蛤蛤蛤蛤蛤蛤蛤蛤蛤蛤蛤</main>
</div>
```


```
div {width: 200px;}
aside {
  background-color: yellow;
  float: left;
  width: 100px;
  height: 50px;
}
main {
  background-color: pink;
}

```

由于左边元素设置了浮动，右侧元素的一部分跑到了左侧元素下方：

![](/assets/1473403826-5925a457e6461_articlex.png)


解决方案：**为main设置 overflow: hidden; 触发main元素的BFC**，根据规则第4、5条，**BFC的区域是独立的，不会与页面其他元素相互影响，且不会与float元素重叠**，因此就可以形成两列自适应布局

![](/assets/908715570-5925a46960096_articlex.png)

3. 防止垂直margin合并

略


## 参考
### 已学习
BFC与IFC概念理解+布局规则+形成方法+用处
https://segmentfault.com/a/1190000009545742

### 待学习

