# Inquirer.js学习与实践

## 一 简介

### 1用途

A collection of common interactive command line user interfaces.

在开发过程中，需要频繁的跟命令行进行交互，借助inquirer模块就能轻松实现，它提供了用户界面和查询会话流程。


### 2优缺点及对比


## 二 基本概念与技术重点整理

inquirer功能简介

input–输入
validate–验证
list–列表选项
confirm–提示
checkbox–复选框等

### 语法
```
var inquirer = require('inquirer')
inquirer.prompt([/* Pass your questions in here */]).then(function (answers) {
    // Use user feedback for... whatever!! 
})
```

## 三 使用实践及案例

初始化项目后安装inquirer

cnpm install inquirer --save

### 一个简单的inquirer例子

可执行命令act文件代码：

```
#! /usr/bin/env node
const program = require('commander')
const inquirer = require('inquirer')
const chalk = require('chalk')

program
  .command('module')
  .alias('m')
  .description('创建新的模块')
  .option('-a, --name [moduleName]', '模块名称')
  .option('--sass', '启用sass')
  .option('--less', '启用less')
  .action(option => {
          var config = Object.assign({
              moduleName: null,
              description: '',
              sass: false,
              less: false
          }, option)
          var promps = []
          if(config.moduleName !== 'string') {
                promps.push({
                  type: 'input',
                  name: 'moduleName',
                  message: '请输入模块名称',
                  validate: function (input){
                      if(!input) {
                          return '不能为空'
                      }
                      return true
                  }
                })
          }
          if(config.description !== 'string') {
              promps.push({
                  type: 'input',
                  name: 'moduleDescription',
                  message: '请输入模块描述'
              })
          }
          if(config.sass === false && config.less === false) {
            promps.push({
              type: 'list',
              name: 'cssPretreatment',
              message: '想用什么css预处理器呢',
              choices: [
                {
                  name: 'Sass/Compass',
                  value: 'sass'
                },
                {
                  name: 'Less',
                  value: 'less'
                }
              ]
            })
          }
          inquirer.prompt(promps).then(function (answers) {
              console.log(answers)
          })
      })
      .on('--help', function() {
          console.log('  Examples:')
          console.log('')
          console.log('$ app module moduleName')
          console.log('$ app m moduleName')
      })

program.parse(process.argv)

```

这里加了

```
inquirer.prompt(promps).then(function (answers) {
              console.log(answers)
          })
```

接受到从用户输入或选择拿到的数据后，输出了结果。

执行命令：

![](/assets/WX20171023-100853@2x.png)

选择完后：

![](/assets/WX20171023-100930@2x.png)



## 四 资源与参考

### 1官网

### 2文档

[https://github.com/SBoudrias/Inquirer.js/\#documentation](https://github.com/SBoudrias/Inquirer.js/#documentation)

### 3源码

[https://github.com/SBoudrias/Inquirer.js/](https://github.com/SBoudrias/Inquirer.js/)

### 4教程

官方教程：

其他教程：

### 5工具与资源



