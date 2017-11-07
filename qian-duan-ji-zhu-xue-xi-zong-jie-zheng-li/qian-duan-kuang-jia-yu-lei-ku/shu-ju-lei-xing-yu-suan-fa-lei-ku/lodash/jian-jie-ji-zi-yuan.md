# lodash 简介使用及资源

## 一 简介
一个具有一致接口、模块化、高性能等特性的 JavaScript 工具库。

### 1用途
####（1）适用场景


### 2优缺点及对比
####（1）优点

####（2）缺点
库略大，压缩前约526KB,压缩后大概占70KB，如果用的不多，或者对性能要求很高，需考虑是否要使用（以及以何种方式引入，比如可以按需引入减小文件提升性能）。

## 二 使用


```
npm i --save lodash
```

引用：


```
// 完全引入
var _ = require('lodash');
// 引入核心
var _ = require('lodash/core');

// 按方法类型部分引入
var array = require('lodash/array');
var object = require('lodash/fp/object');

// 按需引入，如果只有少量的部分方法，此方法在browserify/rollup/webpack构建打包后size最小
var at = require('lodash/at');
var curryN = require('lodash/fp/curryN');
```

### 按需引用
**如果只用少量的部分方法，建议按需引入（就引入该方法定义的文件），性能更好（特别是对移动端页面），如：**

```
import clone from 'lodash/clone';
```

### 引用核心core
如果用的方法都在核心里，也可以引用核心core方法（gzip压缩后只有4kb）

```
// 引入核心
var _ = require('lodash/core');
```

核心core模块包含的方法清单见：
https://github.com/lodash/lodash/wiki/Build-Differences


## 资源与参考

### 1官网
https://lodash.com

### 2文档
官方文档（推荐）
https://lodash.com/docs

中文文档（版本可能会滞后于英文版，推荐直接去看上面的英文文档）
http://lodashjs.com/docs/

### 3源码
https://github.com/lodash/lodash

### 4教程
#### （1）已学习：


#### （2）学习中：


#### （3）待学习：
官方教程：

其他教程：

### 5工具与资源



