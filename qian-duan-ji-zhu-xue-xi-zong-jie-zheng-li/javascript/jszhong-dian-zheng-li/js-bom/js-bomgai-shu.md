# window对象

## 一 概述
window对象指当前的浏览器窗口。

JS规定，浏览器环境的所有全局变量，都是window对象的属性。

## 二 window对象的属性
window.window属性指向自身
window.name用于设置当前浏览器窗口的名字

### 1 window.location
**window.location**返回一个location对象，用于**获取窗口当前的URL信息**。等同document.location。

### 2 window 尺寸相关属性
#### （1） window.screenX，window.screenY
返回浏览器窗口左上角相对于当前屏幕左上角（(0, 0)）的水平距离和垂直距离，单位为像素

#### （2） window.innerHeight，window.innerWidth
**window.innerHeight和window.innerWidth属性，返回网页在当前窗口中可见部分的高度和宽度**，即“视窗”（viewport），单位为像素。

注意，这两个属性值包括滚动条的高度和宽度。

#### （3） window.outerHeight，window.outerWidth
返回**浏览器窗口的高度和宽度**，包括浏览器菜单和边框，单位为像素。

#### （4） window.pageXOffset，window.pageYOffset
window.pageXOffset 返回页面的水平滚动距离window.pageYOffset 返回页面的垂直滚动距离
单位像素

### 3 window.screen对象
window.screen对象包含了显示设备的信息。

screen.height和screen.width两个属性，一般用来了解**设备的分辨率**。

screen.availHeight和screen.availWidth属性返回屏幕可用的高度和宽度。值为屏幕的实际大小减去操作系统某些功能的空间，如系统的任务栏。


### 4 window.navigator对象
指向一个包含**浏览器信息**的对象。

#### （1）navigator.userAgent
浏览器的User-Agent字符串，标示浏览器的厂商和版本信息。

通过userAgent识别浏览器，不是一个好办法。所以，现在一般不再识别浏览器了，而是使用“功能识别”方法，即逐一测试当前浏览器是否支持要用到的JS功能。

不过，通过userAgent可以大致准确地识别手机浏览器，方法就是测试是否包含mobi字符串。

```
var ua = navigator.userAgent.toLowerCase();

if (/mobi/i.test(ua)) {
  // 手机浏览器
} else {
  // 非手机浏览器
}
```


如果想要识别所有移动设备的浏览器，可测试更多的特征字符串。

```
/mobi|android|touch|mini/i.test(ua)
```

#### （2）navigator.platform
返回用户的操作系统信息

#### （3）navigator.geolocation
返回Geolocation对象，包含用户地理位置的信息。

## 三 window对象的方法
### 1 window.moveTo()，window.moveBy()
window.moveTo() 移动浏览器窗口到指定位置
window.moveBy() 将窗口移动到一个相对位置(相对于当前位置)

### 2 window.scrollTo()，window.scrollBy()

window.scrollTo（别名window.scroll）方法 将网页的指定位置，滚动到浏览器左上角。参数是相对于整张网页的横坐标和纵坐标。

window.scrollBy() 将网页移动指定距离，单位为像素。两参数：向右滚动的像素，向下滚动的像素。

### 3 window.open(), window.close()
window.open()：新建另一个浏览器窗口，并且返回该窗口对象。

一共可接受四个参数。

参数一：字符串，表示新窗口的网址。
参数二：字符串，表示新窗口的名字。
参数三：字符串，内容为逗号分隔的键值对，表示新窗口的参数，比如有没有提示栏、工具条等等。如省略，则打开一个完整UI的新窗口。
参数四：布尔值，表示第一个参数指定的网址，是否应该替换history对象之中的当前网址记录，默认值为false。

window.close方法用于关闭当前窗口，一般用来关闭window.open方法新建的窗口。

## 四 window对象的事件
### 1 load事件和onload属性
load事件发生在文档在**浏览器窗口加载完毕**时。**window.onload属性可以指定这个事件的回调**函数。

```
window.onload = function() {
    // ...
};
```

上面代码在网页加载完毕后进行一些处理。

### 2 error事件和onerror属性
浏览器脚本发生错误时，会触发window对象的error事件。可通过window.onerror属性对该事件指定回调函数。

## 五 alert()，confirm()，prompt()（浏览器与用户互动的全局方法）
alert() 弹出的对话框，只有一个“确定”按钮，往往用来通知用户某些信息。

confirm() 弹出的对话框，除了提示信息之外，只有“确定”和“取消”两个按钮，往往用来征询用户的意见。

prompt() 弹出的对话框，在提示文字的下方，还有一个输入框，要求用户输入信息，并有“确定”和“取消”两个按钮。它往往用来获取用户输入的数据。


## 参考

###已学习 
window对象（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/bom/window.html

###未学习
