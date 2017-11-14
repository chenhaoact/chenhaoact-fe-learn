# css-modules
## 简介
CSS Modules 不是将 CSS 改造成编程语言，而是功能很单纯，只加入了局部作用域和模块依赖，这恰恰是网页组件最急需的功能。

### 1. 局部作用域
一般而言，CSS的规则都是全局的，任何一个组件的样式规则，都对整个页面有效。

产生局部作用域的唯一方法，就是用一个独一无二的class名，不与其他选择器重名。这也是 CSS Modules 的做法。

**引入CSS Modules后构建工具会将类名编译成一个独一无二的哈希字符串。**

### 2. 全局作用域
使用`:global(.className)`语法，声明一个全局规则。凡是这样声明的class，都不会被编译成哈希字符串。

### 3. 定制哈希类名（可以根据需求定制方便调试）

如：在webpack的loaders的css配置中这样设置：

```
{
      test: /\.css$/,
      loader: "style-loader!css-loader?modules&localIdentName=[path][name]---[local]---[hash:base64:5]"
    },
```

`.title`类就能被编译成类似于`demo03-components-App---title---GpMto`这样的类名，这样调试定位起来就比较清晰，不会因为只有一堆哈希值二无法查询是哪里定义的样式类。

### 4. 样式继承

通过样式定义中的composes属性
```
composes: 要继承的className;
```

继承了.className的样式。

### 5. 变量引用

CSS Modules 支持使用变量，不过需要安装 PostCSS 和 postcss-modules-values。

使用`@`定义变量。


## 使用

在webpack的loaders的css配置中加一个查询参数modules，表示打开 CSS Modules 功能:

```
{
        test: /\.css$/,
        loader: "style-loader!css-loader?modules"
      }
```

## 插件

### react-css-modules（让react项目中接入css-module使用起来更方便）
https://github.com/gajus/react-css-modules

## 参考
### 已学习
CSS Modules 用法教程-阮一峰
http://www.ruanyifeng.com/blog/2016/06/css_modules.html

### 待学习