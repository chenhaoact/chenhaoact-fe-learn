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

块级元素在代码中如果有换行会自动加上一点外边距(默认加了空格或换行符)，导致自适应被打乱，这里使用设置ul的font-size:0消除。

具体参考：
如何解决inline-block元素的空白间距
https://www.w3cplus.com/css/fighting-the-space-between-inline-block-elements


## 二 瀑布流

## 1. 各块定宽不定高，自适应排布

