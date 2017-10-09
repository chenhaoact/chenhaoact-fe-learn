## 一 React整体目录分析

从https://github.com/facebook/react git clone 源代码到本地，打开看到如下目录：

![](/assets/WX20170809-161417@2x.png)

源代码在src下，阅读源码主要读src目录下的代码即可。在此之前，先简单解析下其他的目录。

### package.json

从这里看项目的依赖以及脚本命令：

![](/assets/WX20171009-185427@2x.png)

运行

```
npm install

```

安装好依赖。

开发构建相关的命令在scripts中（里面定义的命令会用到scripts目录下的配置文件），react采用[jest](https://facebook.github.io/jest/)进行测试，配置在jest下。

这里的命令作用：

npm run bench
npm run build ：项目构建
npm run lint ：代码校验.
npm test ：使用[jest](https://facebook.github.io/jest/)进行整体测试（测试脚本定义在jest下）
npm test <pattern> ：测试某类文件
npm run flow ：使用[flow](https://flow.org/)进行类型检查
npm run prettier： 使用[prettier](https://github.com/prettier/prettier)进行代码格式化

### scripts目录

scripts目录定义了项目开发构建等命令脚本的配置：

![](/assets/WX20170809-173651@2x.png)

### build目录

完成react源代码编写与测试后，执行：


```
npm run build
```

会生产react相关的文件：

![](/assets/WX20170810-110250@2x.png)

![](/assets/WX20171009-190450@2x.png)


**注意！这里构建生产的文件（build/packages下的文件）就是我们在开发react项目中通过npm install react npm install react-dom 等命令安装在node_modules 下的源文件。**


### CHANGELOG.md 更新日志

从这里可以了解到React各个历史版本的重要更新点，是了解React版本迭代与技术演进的一个途径。

比如：

**在 2017年9月28号的15.6.2版本，协议由BSD更改为MIT**：

![](/assets/WX20171007-143810@2x.png)

### docs目录

各种项目文档。

![](/assets/WX20170809-174144@2x.png)

### eslint-rules目录

eslint的一些规则。

![](/assets/WX20170809-174308@2x.png)


### fixtures目录

React固有特性

![](/assets/WX20171009-190033@2x.png)

包括像dom以及React 16很重要的一个更新 **[React fiber](https://github.com/acdlite/react-fiber-architecture)**,这里的几个目录内都可以用 npm install 和 npm start跑起来看效果的。

### flow目录
[flow](https://flow.org/) 类型检查的一些配置。

![](/assets/WX20171009-190204@2x.png)

### mocks目录
模拟了简单的用于测试的React组件和子组件。

### packages目录
**react构建时在此目录基础下进行生产，可以看到这里的目录结构和build目录下的packages（最终用于开发者开发时npm安装的文件）结构一样。**

![](/assets/WX20170810-113357@2x.png)


### src目录
react源码开发目录，后面会具体分析。

![](/assets/WX20170810-135047@2x.png)









