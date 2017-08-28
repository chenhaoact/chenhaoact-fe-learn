# History对象

## 一 简介
浏览器窗口有一个**history对象**，用来保存**浏览历史**。

## 二 history属性
### history.length
当前**窗口先后访问了三个网址，那么history对象就包括三项，history.length属性等于3**。

## 三 history方法
### 1 back() forward() go()
history对象提供了一系列方法，允许在浏览历史之间移动。

back()：移动到上一个访问页面，等同于浏览器的后退键。

forward()：移动到下一个访问页面，等同于浏览器的前进键。

go()：接受一个整数作为参数，移动到该整数指定的页面，比如go(1)相当于forward()，go(-1)相当于back()。

### 2 HTML5新加的 history.pushState() 和 history.replaceState()

HTML5为history对象添加了两个新方法，history.pushState()和history.replaceState()，用来在浏览历史中添加和修改记录。



## 参考

###已学习 
History对象（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/bom/history.html

###未学习