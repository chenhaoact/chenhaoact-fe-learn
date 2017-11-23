## 使用
### 1. 设置断点
打开source，找到要断点调试的文件（配置了了webpack devtool的在webpack目录下），在行前面点击打断点，这样程序允许时就会允许到各个断点上暂停，点下一步时才会往下一个断点运行，这样可以找出报错等信息究竟是在程序的哪里出现的，更快速的定位问题。
![](/assets/WX20171123-091224@2x.png)

### 2. 观察运行中各个变量的值
**运行断点前的所有变量的值都会在chrome中显示**（每一行代码后面后显示，同时鼠标覆盖上去也会出现改变量的详细值），**方便在程序运行时观察每个变量的值，不用再在程序里通过console.log的方式一个一个打出来（太低效了**）。
![](/assets/WX20171123-091959@2x.png)


## 参考
### 待学习
如何设置断点(包括dom端点调试)
https://developers.google.com/web/tools/chrome-devtools/javascript/add-breakpoints?hl=zh-cn

