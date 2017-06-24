http://www.iconfont.cn/

web上目前推荐**symbol引用**

这是一种全新的使用方式，应该说这才是未来的主流，也是平台目前推荐的用法。这种用法其实是做了一个svg的集合，与上面两种相比具有如下特点：

优点：
**支持多色图标**了，不再受单色限制。
通过一些技巧，支持像字体那样，通过font-size,color来调整样式。

缺点：
兼容性较差，支持 ie9+,及现代浏览器。
**浏览器渲染svg的性能一般，还不如png**。

使用步骤如下：

第一步：拷贝项目下面生成的symbol代码：

//at.alicdn.com/t/font_1473319176_4914331.js
第二步：加入通用css代码（引入一次就行）：

<style type="text/css">
    .icon {
       width: 1em; height: 1em;
       vertical-align: -0.15em;
       fill: currentColor;
       overflow: hidden;
    }
</style>
第三步：挑选相应图标并获取类名，应用于页面：

<svg class="icon" aria-hidden="true">
    <use xlink:href="#icon-xxx"></use>
</svg>


如果是在**react项目中引入的话，这里的xlink:href需要改成xlinkHref,class要改成className才会起作用。aria-hidden则不需要改成驼峰法**

具体的图标样式可以参考：svg中use元素引用symbol样式的思考
http://blog.csdn.net/xiaozhu2hao/article/details/53183743


iconfont各个场景下的图标使用步骤具体参考：

http://www.iconfont.cn/help/detail?spm=a313x.7781069.1998910419.d8cf4382a.qUloTK&helptype=code
