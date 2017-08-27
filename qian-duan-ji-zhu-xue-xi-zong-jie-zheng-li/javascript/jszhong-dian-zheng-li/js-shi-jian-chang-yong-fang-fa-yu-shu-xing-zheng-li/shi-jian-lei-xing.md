# js事件类型整理

## 一 鼠标事件
### click 事件 
“鼠标单击”定义为，用户在同一个位置完成一次mousedown动作和mouseup动作。触发顺序是：mousedown首先触发，mouseup接着触发，click最后触发。

设置click事件监听函数的例子：

```
div.addEventListener("click", function( event ) {
  // 显示在该节点，鼠标连续点击的次数
  event.target.innerHTML = "click count: " + event.detail;
}, false);
```

### mouseup，mousedown，mousemove 事件

mouseup事件 释放按下的鼠标键时触发。

mousedown事件 在按下鼠标键时触发。

mousemove事件 当鼠标在一节点内移动时触发。当鼠标持续移动，该事件连续触发。为了避免性能问题，建议对该事件的监听函数做一些限定，如限定一段时间内只运行一次代码。

###mouseover 事件，mouseenter 事件
mouseover和mouseenter事件，都是**鼠标进入一个节点时触发**。

两者区别：
**mouseenter事件只触发一次**，而只要鼠标在节点内部移动，mouseover事件会在子节点上触发多次。

### mouseout，mouseleave 事件
mouseout和mouseleave事件，都是**鼠标离开一个节点时触发**。

两者的区别：
**子节点的mouseout事件会冒泡到父节点，进而触发父节点的mouseout事件**。mouseleave事件就没有这种效果，离开子节点时，不会触发父节点的监听函数。

### contextmenu 事件
在一个节点上点击鼠标右键时触发。

### MouseEvent 对象
鼠标事件使用MouseEvent对象表示，它继承UIEvent对象和Event对象。浏览器提供一个MouseEvent构造函数，用于新建一个MouseEvent实例。

具体可参考：
http://javascript.ruanyifeng.com/dom/event-type.html#toc6

## 二 鼠标滚轮（wheel）事件
wheel事件是与鼠标滚轮相关的事件，目前只有一个**wheel事件。用户滚动鼠标的滚轮，就触发这个事件**。

该事件除了继承了MouseEvent、UIEvent、Event的属性，还有几个自己的属性（如滚轮的水平滚动量，滚轮的垂直滚动量等）。

## 三 键盘事件

键盘事件用来描述键盘行为，主要有**keydown、keypress、keyup**三个事件：

keydown：按下键盘时触发该事件。

keypress：只要按下的键并非Ctrl、Alt、Shift和Meta，就接着触发keypress事件。

keyup：松开键盘时触发该事件。

如果用户一直按键不松开，就会连续触发键盘事件，触发的顺序为：

keydown
keypress
keydown
keypress
（重复以上过程）
keyup

## 四 触摸事件

触摸API由三个对象组成。

Touch：Touch对象表示触摸点（**一根手指**或者一根触摸笔），用来描述触摸动作，包括位置、大小、形状、压力、目标元素等属性。

TouchList：TouchList对象是一个类似数组的对象，**成员是与某个触摸事件相关的所有触摸点**。如，用户用三根手指触摸，产生的TouchList对象就有三个成员，每根手指对应一个Touch对象。

TouchEvent：TouchEvent对象继承Event对象和UIEvent对象，表示触摸引发的事件。除了被继承的属性以外，它还有一些自己的属性。

### 触摸事件的种类
触摸引发的事件，有以下几类。可以通过TouchEvent.type属性，查看到底发生的是哪一种事件。

touchstart：用户接触触摸屏时触发，它的target属性返回发生触摸的Element节点。

touchend：用户不再接触触摸屏时（或者移出屏幕边缘时）触发，它的target属性与touchstart事件的target属性是一致的，它的changedTouches属性返回一个TouchList对象，包含所有不再触摸的触摸点（Touch对象）。

touchmove：用户移动触摸点时触发，它的target属性与touchstart事件的target属性一致。如果触摸的半径、角度、力度发生变化，也会触发该事件。

touchcancel：触摸点取消时触发，比如在触摸区域跳出一个情态窗口（modal window）、触摸点离开了文档区域（进入浏览器菜单栏区域）、用户放置更多的触摸点（自动取消早先的触摸点）。



## 五 拖拽事件
拖拽：用户在某对象上按下鼠标键不放，拖动它到另一个位置，然后释放鼠标键，将该对象放在那里。

在HTML网页中，除了Element节点默认不可以拖拉，其他（图片、链接、选中的文字）都是可以直接拖拽的。**为了让Element节点可拖拽，可将draggable属性设为true**。

```
<div draggable="true">
  此区域可拖拽
</div>
```

draggable属性可用于任何Element节点，但是图片（img元素）和链接（a元素）默认就可以拖拽。对于它们，用到这个属性的时候，往往是将其设为false，防止拖拽。

注意：一旦某个Element节点的draggable设为true，就无法再用鼠标选中该节点内部的文字或子节点了。

### 拖拽事件种类
当Element节点或选中的文本被拖拉时，就会持续触发拖拉事件，包括以下事件：

drag事件：拖拉过程中，在被拖拉的节点上持续触发。

dragstart事件：拖拉开始时在被拖拉的节点上触发，该事件的target属性是被拖拉的节点。通常应该在这个事件的监听函数中，指定拖拉的数据。

dragend事件：拖拉结束时（释放鼠标键或按下escape键）在被拖拉的节点上触发。

dragenter事件：拖拉进入当前节点时，在当前节点上触发。通常应该在这个事件的监听函数中，指定是否允许在当前节点放下（drop）拖拉的数据。

dragover事件：拖拉到当前节点上方时，在当前节点上持续触发。

dragleave事件：拖拉离开当前节点范围时，在当前节点上触发，该事件的target属性是当前节点。

drop事件：被拖拉的节点或选中的文本，释放到目标节点时，在目标节点上触发。

### DataTransfer对象
所有的拖拉事件都有一个dataTransfer属性，用来保存需要传递的数据。这个属性的值是一个DataTransfer对象。有各种设置数据，文件的属性与方法。

具体可参考：
http://javascript.ruanyifeng.com/dom/event-type.html#toc19


## 六 表单事件

### Input事件，select事件，change事件

这些事件与表单成员的值变化有关。

（1）input事件

input事件当`<input>、<textarea>`的值发生变化时触发。

input事件的一个特点，就是会连续触发，比如用户每次按下一次按键，就会触发一次input事件。

（2）select事件

select事件当在`<input>、<textarea>`中选中时触发。



```
var elem = document.getElementById('test');
elem.addEventListener('select', function() {
  console.log('Selection changed!');
}, false);
```

（3）Change事件

Change事件当`<input>、<select>、<textarea>`的值发生变化时触发。**它与input事件的最大不同，就是不会连续触发，只有当全部修改完成时才会触发**，而且input事件必然会引发change事件。具体来说，分成以下几种情况。

激活单选框（radio）或复选框（checkbox）时触发。
用户提交时触发。比如，从下列列表（select）完成选择，在日期或文件输入框完成选择。
当文本框或textarea元素的值发生改变，并且丧失焦点时触发。


### reset事件，submit事件
以下事件发生在表单对象上，而不是发生在表单的成员上。

（1）reset事件

reset事件当表单重置（所有表单成员变回默认值）时触发。

（2）submit事件

submit事件当表单数据向服务器提交时触发。注意，submit事件的发生对象是form元素。

## 七 进度事件（ProgressEvent）

进度事件：
用来描述一个事件进展的过程，如：HTTP请求的过程、`<img>、<audio>、<video>、<style>、<link>`加载外部资源的过程。下载和上传都会发生进度事件。

进度事件有以下几种：

abort事件：当进度事件被中止时触发。如果发生错误，导致进程中止，不会触发该事件。

error事件：由于错误导致资源无法加载时触发。

load事件：进度成功结束时触发。

loadstart事件：进度开始时触发。

loadend事件：进度停止时触发，发生顺序排在error事件\abort事件\load事件后面。

progress事件：当操作处于进度之中，由传输的数据块不断触发。

timeout事件：进度超过限时触发。

应用实例：


```
image.addEventListener('load', function(event) {
  image.classList.add('finished');
});

image.addEventListener('error', function(event) {
  image.style.display = 'none';
});
```


上面代码在图片加载完后，为图片元素的class属性添加“finished”。如加载失败，就把图片元素的样式设置为不显示。

有时，图片加载会在脚本运行之前就完成，因此有可能使得load和error事件的监听函数根本不会被执行。比较可靠的方式是用complete属性先判断一下是否加载完成。

## 八 文档及其他事件
### scroll，resize事件
这些事件与窗口行为有关。

（1）scroll事件

**scroll事件在文档或文档元素滚动时触发**，主要出现在用户拖动滚动条。



```
window.addEventListener('scroll', callback);
```


由于该事件会连续地大量触发，所以它的监听函数之中不应该有非常耗费计算的操作。推荐的做法是使用requestAnimationFrame或setTimeout控制该事件的触发频率，然后可以结合customEvent抛出一个新事件。

（2）resize事件

**resize事件在改变浏览器窗口大小时触发**，发生在window、body、frameset对象上面。

该事件也会连续地大量触发，所以最好像上面的scroll事件一样，通过throttle函数控制事件触发频率。

### 焦点事件
焦点事件发生在Element节点和document对象上面，与获得或失去焦点相关。主要包括以下几个事件：

focus事件：Element节点获得焦点后触发，该事件不会冒泡。

blur事件：Element节点失去焦点后触发，该事件不会冒泡。

##参考
### 已学习
事件类型（javascript标准参考教程，阮一峰）
http://javascript.ruanyifeng.com/dom/event-type.html

### 待学习









