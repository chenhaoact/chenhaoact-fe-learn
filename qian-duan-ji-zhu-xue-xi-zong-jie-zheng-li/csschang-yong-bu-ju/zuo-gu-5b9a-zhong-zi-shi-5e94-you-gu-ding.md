# 三栏布局（左固定-中自适应-右固定）

## 一 左固定-中自适应-右固定 布局的实现方法
### 1 左元素与右元素分别定宽想左右浮动，中间元素放在最后（注意放置顺序不能反）



```html
<div class="layout1">
  <div class="floatLeft">左固定宽度</div>
  <div class="floatRight">右固定宽度</div>
  <div class="content">中自适应宽度</div>
</div>
```



```less
@layout1Height: 100px;
@layout1Width: 500px;

.layout1{
  width: @layout1Width;
  overflow: hidden;
  color: white;
  
  .floatLeft{
    float: left;
    width: 100px;
    height: @layout1Height;
    background: blue;
  }
  
  .floatRight{
    float: right;
    width: 100px;
    height: @layout1Height;
    background: green;
  }
  
  .content{
    height: @layout1Height;
    background: red;
    overflow: hidden;
  }
  
}

```

![](/assets/WX20171018-175517@2x.png)

**codepen效果演示：
**

https://codepen.io/chenhaoact/pen/BwvVoW/


## 二 圣杯布局
TODO

## 三 双飞翼布局
TODO

## 参考
### 待学习
CSS || 三栏布局，两边固定，中间自适应
https://segmentfault.com/a/1190000008705541

CSS布局 -- 圣杯布局 & 双飞翼布局
http://www.cnblogs.com/imwtr/p/4441741.html