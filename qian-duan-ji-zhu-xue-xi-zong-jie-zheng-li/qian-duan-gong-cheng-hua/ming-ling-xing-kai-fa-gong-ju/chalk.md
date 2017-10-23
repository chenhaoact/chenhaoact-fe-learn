# chalk
## 一 简介
可以让命令行写出各种样式，美化命令行的模块，它具有轻量级、高性能、学习成本低等特点

## 二 使用

### 1 设置console.log的颜色

```
const chalk = require('chalk')

...
 console.log(chalk.green('开始创建一个act项目'))
 console.log(chalk.blue.bgRed('act项目创建成功')) //支持设置背景
...
 
```

便能够在命令行打出响应文字的时候，展示出特定的样式，如：

![](/assets/WX20171023-102646@2x.png)








## 参考
### 官方资源
https://github.com/chalk/chalk

### 教程
跟着老司机玩转Node命令行
https://aotu.io/notes/2016/08/09/command-line-development/index.html




