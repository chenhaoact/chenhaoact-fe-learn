# jset-令人愉快的 JavaScript 测试

## 一 简介

### 1用途
####（1）适用场景
尤其适合react，react native相关应用的js测试。

### 2优缺点及对比
####（1）优点
**设置简单。**完整且只需建议设置的 JavaScript 测试解决方案。任何React程序都能从容使用。

**即时反馈。**快速交互式监视模式仅运行到更改的相关文件并能快速发出信号。

**支持快照测试（snapshots test）。**捕获快照反应树或其他可序列化的值来简化测试和分析状态如何随时间的变化。

**零配置测试。**Jest 被 Facebook 用来测试包括 React 应用在内的所有 JavaScript 代码。Jest 的一个理念是提供**一套完整集成的 “零配置” 测试体验**。我们发现，当向开发人员提供了现成可用的工具后，他们会愿意写更多的测试，这也使得他们的代码库更加稳定和健康。**在你使用 create-react-app 或 react-native init 创建你的 React 或 React Native 项目时，Jest 都已经被配置好并可以使用了**。**在 __tests__文件夹下放置你的测试用例，或者使用 .spec.js 或 .test.js 后缀给它们命名**。不管你选哪一种方式，Jest 都能找到并且运行它们。

**高速和沙盒**。Jest 跨工人以最大化性能并行化的测试运行。控制台消息都是缓冲并输出测试结果。沙盒测试文件和自动全局状态将为每个测试重置，因此**测试代码间不会冲突**。

**内置代码覆盖率报告。**使用 ' --coverage ' 参数来轻松地创建代码覆盖率报告。无需额外安装程序或代码库 ！Jest 可以从整个项目包括未经测试的文件收集代码覆盖率信息。

**拥有功能强大的模拟库。**强大的[模拟代码库](http://facebook.github.io/jest/docs/mock-functions.html) 函数和模块。使用 jest-react-native来模拟React Native组件。

**可与Typescript等一同使用。**Jest可以使用于任何Javascript编译器，与Babel Typescript通过 ts-jest无缝集成。

####（2）缺点


## 二 基本概念与技术重点整理

### 快照测试(snapshots test)
参考：
http://facebook.github.io/jest/docs/zh-Hans/snapshot-testing.html#content

## 三 使用实践及案例

###1 安装并写一个简单的jest测试

通过npm 来安装Jest︰


```
npm install --save-dev jest

```


或者通过yarn：


```
yarn add --dev jest

```



从写一个两个数相加的示例函数开始。首先，创建一个 sum.js 文件︰



```
function sum(a, b) {
  return a + b;
}
module.exports = sum;

```


然后，创建一个名为 sum.test.js 的文件。这将包含我们的实际测试︰


```
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});

```
此测试使用 expect 和 toBe 来测试两个值完全相同。 若要了解Jest关于测试方面更多的能力，请参阅 [Using Matchers](http://facebook.github.io/jest/docs/using-matchers.html)。

将下面的配置部分添加到你的 package.json 里面：

```
{
  "scripts": {
    "test": "jest"
  }
}

```


运行 npm test，Jest将会打印测试消息。

###2 更多配置
####使用 Babel
要使用 Babel，需安装 babel-jest 和 regenerator-runtime：


```
npm install --save-dev babel-jest regenerator-runtime

```

注意：如果使用了 npm 3 或 4，或 Yarn，就不用再显式安装 regenerator-runtime。

别忘了在项目根文件夹下添加一个 [.babelrc](https://babeljs.io/docs/usage/babelrc/) 配置文件。 比如，如果你正在通过 babel-preset-es2015 和 babel-preset-react 这两个 presets 来使用 ES6 和 React.js:



```
{
  "presets": ["es2015", "react"]
}
```



现在就完成了使用所有 ES6 特性和 React 特殊语法所需的配置。

注意：如果你正在使用一个更复杂的 Babel 配置，并使用 Babel 的 env 选项，请记住 Jest 将会自动定义 NODE_ENV 为 test。 它不会像 Babel 那样在 NODE_ENV 没有被设置时默认使用 development。

注意：当你安装 Jest 时，babel-jest 是会被自动安装的，并且如果你的项目下存在一个 Babel 配置文件时，它将会自动对相关文件进行转义。 如果要避免这个行为，你可以显式的重置 transform 配置项：



```
// package.json
{
  "jest": {
    "transform": {}
  }
}
```


####使用 webpack
Jest 可用于使用 webpack 来管理资源、 样式和编译的项目中。 webpack 与其他工具相比多了一些独特的挑战。 参考 webpack 指南 来开始起步。
使用 TypeScript #
要在测试用例中使用 TypeScript，需要安装 ts-jest 包和 jest 的 types。
npm install --save-dev ts-jest @types/jest
然后修改你的 package.json文件，加入 jest 的相关配置，类似下面这样：
{
  "jest": {
    "transform": {
      "^.+\\.tsx?$": "<rootDir>/node_modules/ts-jest/preprocessor.js"
    },
    "testRegex": "(/__tests__/.*|\\.(test|spec))\\.(ts|tsx|js)$",
    "moduleFileExtensions": [
      "ts",
      "tsx",
      "js",
      "json"
    ]
  }
}


## 

## 四 资源与参考

### 1官网
https://facebook.github.io/jest/

官网中文版
http://facebook.github.io/jest/zh-Hans/

### 2文档
http://facebook.github.io/jest/docs/zh-Hans/getting-started.html

### 3源码
https://github.com/facebook/jest

### 4教程
#### （1）已学习：



#### （2）学习中：



#### （3）待学习：
官方教程：
http://facebook.github.io/jest/docs/zh-Hans/getting-started.html

其他教程：

### 5工具与资源



