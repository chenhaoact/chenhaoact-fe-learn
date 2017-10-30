#移动设备API
## 1.移动设备交互事件（重要）
###（1）touch事件（触摸交互控制）:
  ev.touches中保存着触摸的手指个数
  ev.touches.length为手指个数
  每个touch都保存着
  触摸事件类型:
      1.touchstart
      2.touchend：(对象只存在于changedTouches中)
      3.touchmove
      4.touchcancel
  每个touch对象都有以下属性
  clientX
  clientY
  identifier
  pageX
  pageY
  screenX
  screenY
  target

详见：
触摸事件-MDN
https://developer.mozilla.org/zh-CN/docs/Web/API/Touch_events

另外**可以使用一些触摸事件的js库提升开发效率**，如：[hammer.js](https://github.com/hammerjs/hammer.js)


## 2.Permission API（查询某接口的用户许可情况）
很多操作需用户许可，如脚本想知道用户位置，或操作摄像头。

**Permissions API用来查询某个接口的许可情况。
**

```
// 查询地理位置接口的许可情况
navigator.permissions.query({ name: 'geolocation' })
.then(function(result) {
  // 状态为 prompt，表示查询地理位置时，
  // 用户会得到提示，是否许可本次查询
  /* result.status = "prompt" */

  // 状态为 granted，表示用户已经给予了许可
  /* result.status = "granted" */
});
```

通过此API，可查询用户态度。当用户已明确拒绝时，不必再询问用户许可。

## 3.Viewport（设置视窗与缩放）

Viewport指的是网页的显示区域，也就是不借助滚动条的情况下，用户可以看到的部分网页大小（视窗）。PC上正常情况下，viewport和浏览器显示窗口是一样大小。但在移动设备上，两者可能不一样大小。

如，**手机浏览器的窗口宽度640像素，这时viewport宽度是640像素**，但网页宽度950像素，此时**浏览器会提供横向滚动条，让用户查看窗口容纳不下的310个像素**。另一种方法则是，**将viewport设成950像素，即浏览器的显示宽度还是640像素，但是网页的显示区域达到950像素，整个网页缩小了**，在浏览器中可以看清楚全貌。这样一来，手机浏览器就可以看到网页在桌面浏览器上的显示效果。

viewport缩放规则，需要HTML网页的head部分指定。



```
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no"/>
</head>
```


**一般移动设备建议设置长上面代码，其指定的viewport缩放规则是，缩放到当前设备的屏幕宽度（device-width），初始缩放比例（initial-scale）为1倍，禁止用户缩放（user-scalable）。**

viewport 全部属性如下。

width: viewport宽度
height: viewport高度
initial-scale: 初始缩放比例
maximum-scale: 最大缩放比例
minimum-scale: 最小缩放比例
user-scalable: 是否允许用户缩放

## 4.Geolocation API（获取用户的地理位置）

检查浏览器是否支持这个接口：

```
if(navigator.geolocation) { 
   // 支持
} else {
   // 不支持
}
```

这个API的支持情况非常好，所有浏览器都支持（包括IE 9+），所以可不要上面代码。

###（1） getCurrentPosition方法（获取用户的地理位置）
使用它需要得到用户的授权，浏览器会跳出一个对话框，询问用户是否许可当前页面获取他的地理位置。须考虑两种情况的回调函数：一种是同意授权，另一种是拒绝授权。如果用户拒绝授权，会抛出一个错误。



```
navigator.geolocation.getCurrentPosition(geoSuccess,geoError);
```

如果用户同意授权，就会调用geoSuccess。


```

function geoSuccess(event) {
   console.log(event.coords.latitude + ', ' + event.coords.longitude);
}
```


**geoSuccess的参数是一个event对象。event有两个属性：timestamp和coords。timestamp属性是一个时间戳，返回获得位置信息的具体时间。coords属性指向一个对象，包含了用户的位置信息**，主要是以下几个值：

coords.latitude：纬度
coords.longitude：经度
coords.accuracy：精度
coords.altitude：海拔
coords.altitudeAccuracy：海拔精度（单位：米）
coords.heading：以360度表示的方向
coords.speed：每秒的速度（单位：米）

大多数桌面浏览器不提供上面列表的后四个值。

## 5.Vibration API（使设备振动）
适用场合是向用户发出提示或警告，游戏中尤其会大量使用。

兼容性还不够好，故需要先使用下面的代码检查该接口是否可用：



```
navigator.vibrate = navigator.vibrate
  || navigator.webkitVibrate
  || navigator.mozVibrate
  || navigator.msVibrate;

if (navigator.vibrate) {
  // 支持
}
```

vibrate方法可以使得设备振动，参数是振动持续的毫秒数。


```

navigator.vibrate(1000);
```


上面代码使设备振动1秒钟。

## 6.Luminosity API（屏幕亮度调节）
不常用，需要请查下面参考资料。

## 7.Orientation API（检测手机的摆放方向，竖放或横放）
先使用下面的代码检测浏览器是否支持该API。




```
if (window.DeviceOrientationEvent) {
  // 支持
} else {
  // 不支持
}
```



**一旦设备的方向发生变化，会触发deviceorientation事件**，可对该事件指定回调函数。




```
window.addEventListener("deviceorientation", callback);
```



回调函数接受一个event对象作为参数。


function callback(event){
	console.log(event.alpha);
	console.log(event.beta);
	console.log(event.gamma);
}

上面代码中，**event事件对象有alpha、beta和gamma三个属性，它们分别对应手机摆放的三维倾角变化**。要理解它们，就要理解手机的方向模型。当手机水平摆放时，使用三个轴标示它的空间位置：x轴代表横轴、y轴代表竖轴、z轴代表垂直轴。event对象的三个属性就对应这三根轴的旋转角度。

alpha：表示围绕z轴的旋转，从0到360度。当设备水平摆放时，顶部指向地球的北极，alpha此时为0。
beta：表示围绕x轴的旋转，从-180度到180度。当设备水平摆放时，beta此时为0。
gramma：表示围绕y轴的选择，从-90到90度。当设备水平摆放时，gramma此时为0。


## 参考
### 已学习
[《JavaScript 标准参考教程（alpha）》，by 阮一峰 浏览器环境-移动设备API](http://javascript.ruanyifeng.com/bom/mobile.html)

### 待学习
触摸事件-MDN
https://developer.mozilla.org/zh-CN/docs/Web/API/Touch_events

hammerjs移动端的触摸手势js库
http://www.jianshu.com/p/81a2da3fc06b
