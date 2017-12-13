# JSDoc

## 一 简介
根据js文件中注释信息，生成Js应用程序API文档的工具。

## 二 使用
项目中安装

```
npm install --save-dev jsdoc
```

全局安装

```
npm install -g jsdoc
```

```
jsdoc yourJavaScriptFile.js
```

### JSDoc注释

JSDoc注释一般应该放置在方法或函数声明之前，必须以/ **开始，以便由JSDoc解析器识别。

JSDoc 注释有一套标准的注释标签，一般以@开头。

如：

```
/**
 * 函数作用描述
 * @returns {string|*}
 * @param {string} title - 书本的标题.
 * @param {string} author - 书本的作者.
 */
```

## 常用的JSDoc注释整理
### @param   参数
别名： @arg、 @argument

### @returns 记录函数的返回值
语法和@param类似

### @todo  记录将要完成的任务

### @class 此函数旨在需要使用"new"关键字调用，即构造函数

别名:@constructor


### @constructs 这个函数成员将成为类的构造函数



## 参考
JSDoc中文文档
http://www.css88.com/doc/jsdoc/

