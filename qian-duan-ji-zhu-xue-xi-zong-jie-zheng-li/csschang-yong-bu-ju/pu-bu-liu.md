# 卡片式布局与瀑布流

## 一 卡片式布局（各块高相同,宽度自适应，可设置每行卡片数量，等宽，等边距占满）



```html
<div class="layout2">
  <ul>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
    <li>card</li>
  </ul>
</div>

```


```less
@layoutWidth: 500px;
@numPerLine: 5; //设置每一行卡片的数目，能够自适应卡片宽度并占满屏幕宽（等宽度，等间距）
@interval: 10 / 2px;
@cardWidth: (@numPerLine) * @interval * 2;

.layout2{
  margin-top:20px;
  color:white;
  width: @layoutWidth;
  
  ul{
    font-size: 0; //注意这里的设置去掉了行级元素因为换行默认的带的外边距
    margin: 0px -@interval;
    
    li{
      font-size:14px; //重新设置子元素的
      background: red;
      height: 100px;
      margin: @interval;
      width: calc(~"(100% - @{cardWidth}) / @{numPerLine}");
      display: inline-block;
    }
  }
}
```

![](/assets/WX20171018-195046@2x.png)

codepen线上预览：
https://codepen.io/chenhaoact/pen/ZXVMbe


**这里注意：**

（1）块级元素在代码中如果有换行会自动加上一点外边距(默认加了空格或换行符)，导致自适应被打乱，这里使用设置ul的font-size:0消除。

具体参考：
如何解决inline-block元素的空白间距
https://www.w3cplus.com/css/fighting-the-space-between-inline-block-elements

（2）这里用到了calc()动态计算卡片的宽度，具体看：

[calc()](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/cssshu-xing-da-quan-ff08-bao-han-css3/clac.md)

## 二 瀑布流

## 1. 各块定宽不定高，自适应排布

### 如果不在乎各块排列的顺序，及前面的块不用显示在最上面，可以参考多列排列（可以通过媒体查询做成列数响应式）

具体参考本文的Multi-columns一节介绍的方法（另外此文的flex布局方法不适用于实战，因为分成了五列，实际开发中是循环去生成的，不太可能去再分列，所以不用看其后两种方法）：
纯CSS实现瀑布流布局（大漠）

https://www.w3cplus.com/css/pure-css-create-masonry-layout.html

codepen效果展示：
https://codepen.io/airen/pen/ybyvEM


## 2.对各块的展示顺序有特殊要求，不能一列一列从上往下排，而要一行一行往下排，CSS的方案就不是很完美和有力了，需要用js去计算，可以使用一些成熟的js库：
masonry
https://github.com/desandro/masonry

isotope
https://github.com/metafizzy/isotope 

vue-waterfall
https://github.com/MopTym/vue-waterfall

### 完美的瀑布流解决方案实践
TODO...














