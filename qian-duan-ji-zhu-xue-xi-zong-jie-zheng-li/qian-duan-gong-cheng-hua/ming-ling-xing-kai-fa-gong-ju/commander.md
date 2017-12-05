# commander
## 一 简介
提供了用户命令行输入和参数解析的强大功能，可以帮助我们简化命令行开发。

## 二 使用

### （1）定义一个可执行命令
1. 创建bin目录，下面添加act（文本文件）按照commander进行配置：

```
const program = require('commander')
const inquirer = require('inquirer')
const chalk = require('chalk')
program
    .command('module')
    .alias('m')
    .description('创建新的模块')
    .option('-a, --name [moduleName]', '模块名称')
    .action(option => {
        console.log('Hello World')
    })
    
program.parse(process.argv)

```

2. 配置package.json的bin字段。它可以用来指定可执行（命令）的文件(如果命令文件是js文件要带.js后缀)，如下配置所示
   
```
"bin": {
   "act": "bin/act"
}
```

3. 执行npm link。
它将会把act这个字段复制到npm的全局模块安装文件夹node_modules内，并创建符号链接（symbolic link，软链接），也就是将 act 的路径加入环境变量 PATH

4. 在主入口文件的最上方添加代码 #!/usr/bin/env node, 表明这是一个可执行的应用

```
#!/usr/bin/env node 

const program = require('commander')
const inquirer = require('inquirer')
const chalk = require('chalk')
program
    .command('module')
    .alias('m')
    .description('创建新的模块')
    .option('-a, --name [moduleName]', '模块名称')
    .action(option => {
        console.log('Hello World')
    })
    
program.parse(process.argv)

```

5. 做好了以上三步后，然后运行命令 act module

输出结果 Hello World，一个命令已经定义好了。

命令执行效果：

![](/assets/WX20171023-101056@2x.png)

### commander的api

command – 定义命令行指令，后面可跟上一个name，用空格隔开，如 .command( ‘act [name] ‘)

alias – 定义一个更短的命令行指令作为别名 ，如执行命令$ act m 与之是等价的

description – 描述，它会在help里面展示

option – 定义参数。它接受四个参数，在第一个参数中，它可输入短名字 -a和长名字–act ,
使用 | 或者,分隔，在命令行里使用时，这两个是等价的，区别是后者可以在程序里通过回调获取到；
第二个为描述, 会在 help 信息里展示出来；
第三个参数为回调函数，他接收的参数为一个string，有时候我们需要一个命令行创建多个模块，就需要一个回调来处理；
第四个参数为默认值

action – 注册一个callback函数,这里需注意目前回调不支持let声明变量

parse – 解析命令行

### commander生成帮助信息
执行 $ act m –help

会自动将description、option的信息显示在help中

也可以通过 加 .on() 来 通过自定义的方式(执行函数)生成帮助信息

```
//自定义帮助信息
    ...
    .action(...)
    .on('--help', function() {
        console.log('  Examples:')
        console.log('')
        console.log('$ act module moduleName')
        console.log('$ act m moduleName')
    })
```




## 参考
commander github仓库
https://github.com/tj/commander.js/

Commander写自己的Nodejs命令
http://blog.fens.me/nodejs-commander/

跟着老司机玩转Node命令行
https://aotu.io/notes/2016/08/09/command-line-development/index.html
