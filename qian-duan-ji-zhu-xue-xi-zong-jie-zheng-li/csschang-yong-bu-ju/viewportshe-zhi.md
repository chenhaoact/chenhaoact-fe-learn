# viewport设置
## 一 简介
viewport 是用户网页的可视区域（视区）。

**手机浏览器**是把页面放在一个虚拟的"窗口"（viewport）中，通常该"窗口"（viewport）比屏幕宽，这样就不用把每个网页挤到很小的窗口中，**用户可以通过平移和缩放来看网页的不同部分**。

**而如果制作的网页已经移动端做了适配，就需要设置Viewport不要再允许用户可以缩放和滑动网页**，这样呈现出来的就一直是移动端友好的布局而非页面的某一部分。

## 二 使用

### 一 设置 Viewport
一个常用的针对移动网页优化过的页面的 **viewport meta 标签**大致如下：


```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
**viewport meta 标签的content属性参数：
**
**width：**控制 viewport 的大小，可以指定的一个值，如 600，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。

height：和 width 相对应，指定高度。

**initial-scale：初始缩放比例**，也即是当页面第一次 load 的时候缩放
比例。

maximum-scale：允许用户缩放到的最大比例。

minimum-scale：允许用户缩放到的最小比例。

**user-scalable：用户是否可以手动缩放。**


## 参考
响应式 Web 设计 - Viewport（菜鸟教程）
http://www.runoob.com/css/css-rwd-viewport.html

移动前端开发之viewport的深入理解
https://www.cnblogs.com/2050/p/3877280.html

在移动浏览器中使用viewport元标签控制布局
https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag


