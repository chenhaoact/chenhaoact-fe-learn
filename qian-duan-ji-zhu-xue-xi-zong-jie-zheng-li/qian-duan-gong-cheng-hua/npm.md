# npm
**Node默认的模块管理器**，用来安装和管理Node模块。

## 一 简介

**PS:国内网络建议使用淘宝cnpm安装所有包（安装更快，不容易报错）    
**[https://npm.taobao.org/](https://npm.taobao.org/)

## 二 技术重点整理

###1 npm init 初始化一个项目，生成package.json文件



```
npm init
```



###2 npm install 安装npm模块



```
npm install 模块名 参数
```

（模块名后面@版本号则为安装特定版本的模块，否则安装最新）

#### 参数：
-g 全局安装
–save 保存到package.json的dependencies，可简化为参数-S
--save-dev 保存到package.json的devDependencies，可简化为参数-D
--production 只安装dependencies字段的模块。（npm install默认会安装dependencies和devDependencies中的所有模块）

#### 全局安装的目录
默认情况下，Npm全局模块都安装在系统目录（比如/usr/local/lib/），普通用户没有写入权限，需要用到sudo命令。

如果没有root权限，要安装全局模块请参考：
http://javascript.ruanyifeng.com/nodejs/npm.html#toc10

### 3 npm uninstall 卸载已安装的模块

参数与npm install基本相同。

### 4 npm update 更新本地安装的模块

如果想更新已安装模块，就要用到npm update命令。

```
npm update
```

它会先到远程仓库查询最新版本，然后查询本地版本。如果本地版本不存在，或者远程版本较新，就会安装。

使用-S或--save参数，可在安装时更新package.json里模块的版本号。

### 5 npm run 执行脚本

package.json文件有一个scripts字段，可以用于指定脚本命令，供npm直接调用。

例子：

```
"scripts": {
    "lint": "jshint **.js",
  }
```

scripts字段指定了命令lint，npm run lint，就会执行jshint **.js。

#### npm run不加任何参数运行
会列出package.json里所有可以执行脚本命令。

#### 关于npm run 命令的环境变量
**npm run命令会自动在环境变量$PATH添加node_modules/.bin目录，所以scripts字段里调用命令时不用加路径，这就避免了全局安装NPM模块**。

npm run会创建一个Shell，执行指定命令，**并临时将node_modules/.bin 加入PATH变量**，**这意味着本地模块可以直接运行**。

例子：


```
$ npm i eslint --save-dev
```

运行上面的ESLint的**npm安装命令，会做两件事**: 
首先，ESLint被安装到当前目录的node_modules子目录；

其次，**node_modules/.bin目录会生成一个符号链接node_modules/.bin/eslint，指向ESLint模块的可执行脚本。**

然后，就可以在package.json的script属性里面，不带路径的引用eslint这个脚本。

```
{
  "name": "Test Project",
  "devDependencies": {
    "eslint": "^1.10.3"
  },
  "scripts": {
    "lint": "eslint ."  //注意这里
  }
}
```

**运行npm run lint的时候，它会自动执行./node_modules/.bin/eslint . 。**

#### 一个命令的输出，是另一个命令的输入 或者 命令同时执行
可以借用Linux系统的管道命令（|），将两个操作连在一起，但更方便的写法是引用其他npm run命令。

例子：



```
"build": "npm run build-js && npm run build-css"
```

上面写法**先运行**npm run build-js，**再运行**npm run build-css，两个**命令中间用&&连**接。

如果希望**两命令同时平行执行，中间用&连**接。

#### npm run命令添加参数
如果要通过npm run命令，将参数传到脚本，则参数之前要加上两个连词线 -- 。

例子



```
"scripts": {
  "test": "mocha test/"
}
```



$ npm run test -- anothertest.js
# 等同于
$ mocha test/ anothertest.js



#### 递归更新
从npm v2.6.1 开始，npm update只更新顶层模块，而不更新依赖的依赖，以前版本是递归更新的，要使用下面的命令：

```
$ npm --depth 9999 update
```




### 4 npm list 以树型结构列出当前项目安装的所有模块，以及它们依赖的模块


```
$ npm list
```

加上global参数，会列出全局安装的模块：



```
$ npm list -global
```

npm list命令也可以列出单个模块：


```
$ npm list underscore
```



### 5 npm publish  将当前模块发布到npmjs.com
执行之前，需要向npmjs.com申请用户名。

$ npm adduser
如果已经注册过，就使用下面的命令登录。

$ npm login
登录以后，就可以使用npm publish命令发布。

$ npm publish
如果当前模块是一个beta版，比如1.3.1-beta.3，那么发布的时候需要使用tag参数，将其发布到指定标签，默认的发布标签是latest。

$ npm publish --tag beta
如果发布私有模块，模块初始化的时候，需要加上scope参数。只有npm的付费用户才能发布私有模块。

$ npm init --scope=<yourscope>
如果你的模块是用ES6写的，那么发布的时候，最好转成ES5。首先，需要安装Babel。

$ npm install --save-dev babel-cli@6 babel-preset-es2015@6
然后，在package.json里面写入build脚本。

"scripts": {
  "build": "babel source --presets babel-preset-es2015 --out-dir distribution",
  "prepublish": "npm run build"
}
运行上面的脚本，会将source目录里面的ES6源码文件，转为distribution目录里面的ES5源码文件。然后，在项目根目录下面创建两个文件.npmignore和.gitignore，分别写入以下内容。

// .npmignore
source

// .gitignore
node_modules
distribution

### 其他npm命令与功能概述

1. npm set 设置环境变量（默认初始化选中的name,email,协议等）。

2. npm config ...  配置npm
如：
npm config list -l 查看 npm 的配置

3. npm info 查看每个模块的具体信息

4. npm search 搜索npm仓库，后面可跟字符串，也可跟正则表达式

5. 

6. 


## 三 package中各个字段的含义与作用


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
### 已学习
npm模块管理器-《JavaScript 标准参考教程（alpha）》，by 阮一峰
http://javascript.ruanyifeng.com/nodejs/npm.html

### 待学习
npm 模块安装机制简介

[http://www.ruanyifeng.com/blog/2016/01/npm-install.html](http://www.ruanyifeng.com/blog/2016/01/npm-install.html)

npm scripts 使用指南

[http://www.ruanyifeng.com/blog/2016/10/npm\_scripts.html](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)

