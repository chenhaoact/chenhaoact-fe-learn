# npm

## 一 简介

**PS:国内网络建议使用淘宝cnpm安装所有包（安装更快，不容易报错）    
**[https://npm.taobao.org/](https://npm.taobao.org/)

## 二 技术重点整理

###1 npm初始化一个项目，生成package.json文件



```
npm init
```



###2 安装指定版本的包：



```
npm install 包名@版本号
```





省略写法：

`npm i -D  包名`  

等效于



```
npm install --save-dev  包名

```


### 更新本地安装包 npm update

如果想更新已安装模块，就要用到npm update命令。



```
npm update
```



它会先到远程仓库查询最新版本，然后查询本地版本。如果本地版本不存在，或者远程版本较新，就会安装。

### 列出所有的包依赖


```
npm list
```



###4 package中各个字段的含义与作用


####license 开源协议
如 ISC,MIT等。

各协议之间的区别可参考：主流开源协议之间有何异同？
https://www.zhihu.com/question/19568896

### 5 package-lock.json（从npm5.0开始有）是什么文件？有什么用？
package.json里面定义的是版本范围（比如^1.0.0），具体跑npm install的时候安的什么版本，要解析后才能决定，这里面定义的依赖关系树，称为逻辑树。node_modules文件夹下才是npm实际安装的确定版本的东西，这里面的文件夹结构可称为物理树。

安装过程中有一些去重算法，会发现逻辑树结构和物理树结构不完全一样。

package-lock.json可理解成对结合了逻辑树和物理树的一个快照，里面有明确的各依赖版本号，实际安装的结构，也有逻辑树的结构。其最大的好处就是能获得可重复的构建，当在CI（持续集成）上重复build的时候，得到的artifact是一样的，因为依赖的版本都被锁住了。在npm5以后，其内容和npm-shrinkwrap.json一模一样。


参考
[译] 理解 NPM 5 中的 lock 文件
https://juejin.im/post/5943849aac502e006b84ce07

npm install 生成的package-lock.json是什么文件？有什么用？
https://www.zhihu.com/question/62331583


## 三 相关工具
### 1. npmtrends 比较各个包在过去几个月或几年的下载数量趋势图（有助于进行技术选型和技术热度调研）
http://www.npmtrends.com/

## 参考：

### 待学习
npm 模块安装机制简介

[http://www.ruanyifeng.com/blog/2016/01/npm-install.html](http://www.ruanyifeng.com/blog/2016/01/npm-install.html)

npm scripts 使用指南

[http://www.ruanyifeng.com/blog/2016/10/npm\_scripts.html](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)

