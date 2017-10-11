## 一 移动端交互事件效果

### 按钮点击效果设置

:active{
 设置按钮点击时的效果
}

pc端的hover不适合用在这里（因为hover是相对鼠标而言的，与手势操作不一样）

但iPhone上需要添加
document.addEventListenner("touchstart", function(){}, false);

或者 在body上添加 ontouchstart="" 属性

因为 Safari默认禁用了元素的active样式，通过上述声明重新激活。