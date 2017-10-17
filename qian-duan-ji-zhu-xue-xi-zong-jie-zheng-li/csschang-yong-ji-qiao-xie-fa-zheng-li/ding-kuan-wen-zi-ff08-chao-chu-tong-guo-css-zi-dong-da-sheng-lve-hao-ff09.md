## 容器定宽，右边是固定大小的元素，左边的文字自适应占满剩余空间，如果超长会自动打...

重点在于 .block中的：
text-overflow: ellipsis; //文字超出打省略号


```html
<body>
 
  <div class="container">
    <div class="inlineWarp">
      <div class="block">
        <span>超长文字超长文字</span>
        <span class="stable-size-element">确定大小元素</span>
      </div>
    </div>
  </div>
</body>
```



```less
@stableSize: 100px; //固定元素的宽

.container{
  width:180px;
  background-color: #ccc;
}

.inlineWarp{
  display: inline-block;
  max-width: 100%;
  line-height: 200px;
  
  .block{
    position: relative;
    display: block;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis; //文字超出打省略号
    padding-right: @stableSize;
  }
  
  .stable-size-element{
    position:absolute;
    width:@stableSize;
    height:@stableSize;
    top:0;
    right:0;
    display:inline-block;
    margin:auto;
  }

}
```

![](/assets/WX20171017-174754@2x.png)

**codepen效果演示：**
https://codepen.io/chenhaoact/embed/RLqYvr



