## 容器定宽(或者百分比自适应宽度)，右边是固定大小的元素，左边的文字自适应占满剩余空间，如果超长会自动打...

重点在于两个都设置了浮动，**外边的容器中是overflow: hidden（这样浮动元素的宽高会参与计算）以及
text-overflow: ellipsis; //文字超出打省略号**


```html
<div class="layout4">
  <div class="floatContent">
    超长文字超长文字超长文字超长文字超长文字超长文字超长文字超长文字
  </div>
  <div class="floatFix">
    定长文字
  </div>
</div>
```



```less
@contentWidth:100px;
@contentMarginRight: 20px;
@minusNumber: @contentWidth + @contentMarginRight;

.layout4{
  width: 30%;
  background: red;
  overflow: hidden;
  
  .floatContent{
    width: calc(~"100% - @{minusNumber}");
    overflow:hidden;
    text-overflow:ellipsis;
    white-space: nowrap; //不换行
    float: left;
  }
  
  .floatFix{
    float: right;
    text-align:right;
    width: contentWidth;
  }
}
```

代码效果：

![](/assets/WX20171024-171734@2x.png)

**codepen效果演示：**
https://codepen.io/chenhaoact/embed/RLqYvr



