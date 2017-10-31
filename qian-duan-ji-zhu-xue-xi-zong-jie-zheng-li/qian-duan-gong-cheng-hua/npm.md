# npm

**PS:国内网络建议使用淘宝cnpm安装所有包（安装更快，不容易报错）    
**[https://npm.taobao.org/](https://npm.taobao.org/)

## 技术重点整理

###1 npm初始化一个项目，生成package.json文件

npm init

###2 安装指定版本的包：

npm install 包名@版本号



省略写法：

npm i -D  包名  

等效于

npm install --save-dev  包名

### 更新本地安装包 npm update

如果想更新已安装模块，就要用到npm update命令。

$ npm update

它会先到远程仓库查询最新版本，然后查询本地版本。如果本地版本不存在，或者远程版本较新，就会安装。


###4 package中各个字段的含义与作用


####license 开源协议
如 ISC,MIT等。

各协议之间的区别可参考：主流开源协议之间有何异同？
https://www.zhihu.com/question/19568896


## 参考：

### 待学习
npm 模块安装机制简介

[http://www.ruanyifeng.com/blog/2016/01/npm-install.html](http://www.ruanyifeng.com/blog/2016/01/npm-install.html)

npm scripts 使用指南

[http://www.ruanyifeng.com/blog/2016/10/npm\_scripts.html](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)

