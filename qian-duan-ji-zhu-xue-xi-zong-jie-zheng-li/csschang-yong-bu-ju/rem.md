# web app使用rem代替px
**rem**是指**相对于根元素的字体大小的单位**。简单的说它就是一个相对单位。看到rem大家一定会想起em单位，**em**是**相对于父元素的字体大小的单位**。它们之间其实很相似，只不过一个计算的规则是依赖根元素一个是依赖父元素计算。

## 二 使用（自己简单的实现，理解即可，不推荐实际项目使用）


```
<script type="text/javascript">
  //originWidth设置设计稿原型的屏幕宽度（此处以ipnoe6 设计稿原型屏幕宽375为例）
  let currentClientWidth, fontValue, originWidth = 375;
  __resize();

  //注册resize事件
  window.addEventListener('resize', __resize, false);

  function __resize() {
    currentClientWidth = document.documentElement.clientWidth;

    //设置屏幕的最大值和最小值
    if (currentClientWidth > 640) {
      currentClientWidth = 640
    }
    if (currentClientWidth < 320){
      currentClientWidth = 320;
    }

    const scale = currentClientWidth/10;

    window.adjustScale = 375/10;

    document.documentElement.style.fontSize = `${scale}px`;
    document.body.style.fontSize = `${12/scale}rem`;
  }
</script>
```



##三 推荐！可以使用的一些通过rem移动端适配的类库
**推荐使用此类库，自己写rem有的处理（比如字体带小数点）没有类库写的完善，而且此库很轻量，不影响性能。**

淘宝提供了一个开源的方案lib-flexible
https://github.com/amfe/lib-flexible


具体使用参考：
lib-flexible官方文档
https://github.com/amfe/lib-flexible/tree/master


使用Flexible实现手淘H5页面的终端适配
https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html


另外：
配合postcss和postcss-pxtorem会更好（实现设计稿上是750，css里就写750px，实现自动换算rem值）
https://github.com/cuth/postcss-pxtorem


## 参考
移动web适配利器-rem
http://www.alloyteam.com/2016/03/mobile-web-adaptation-tool-rem/

移动端页面开发适配 rem布局原理
https://segmentfault.com/a/1190000007526917

CSS3的REM设置字体大小
https://www.w3cplus.com/css3/define-font-size-with-css3-rem