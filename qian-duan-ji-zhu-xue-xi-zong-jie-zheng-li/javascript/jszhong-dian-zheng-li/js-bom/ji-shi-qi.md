# js计时器

## setTimeout() 和 clearTimeout()
通过使用 JS，有能力做到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。称之为计时事件。

setTimeout()
未来的某时执行代码

clearTimeout()
取消setTimeout()


```
timedCountTodo = ()=>{
//计时器要执行的逻辑
}

t=setTimeout("timedCountTodo",1000)


function stopCount()
 {
   clearTimeout(t)
 }
```


## setInterval()和clearInterval()
setInterval() 方法可**按照指定的周期**（以毫秒计）来调用函数或计算表达式。

setInterval() 方法会不停地调用函数，

语法：
setInterval(code,millisec[,"lang"])
参数	描述
code	必需。要调用的函数或要执行的代码串。
millisec	必须。周期性执行或调用 code 之间的时间间隔，以毫秒计。

返回值
一个可以传递给 Window.clearInterval() 从而取消对 code 的周期性执行的值。

```
var int= setInterval("clock()",50)
function clock()
  {
  //定时执行的逻辑
  }
</script>

...
//清除setInterval指定的事件
window.clearInterval(int)

```







