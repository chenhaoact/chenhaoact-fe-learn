# eslint使用实践

## 安装和配置ESLint



```
npm install eslint --save-dev
```

配置 .eslintrc 和 .eslintignore文件。


ES6项目还需安装和配置 [babel-eslint](https://github.com/babel/babel-eslint)

可以在根目录下创建一个eslint.js，定义一些eslint的脚本配置，然后在项目 npm run dev和 npm run build的命令前加入 node eslint.js ，这样每次构建之前先进行eslint的校验，不通过则会先退出并提示。



## React项目接入ESLint

安装并配置 [eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)

安装后，react组件需要以 .jsx 结尾（这样可以讲react组件和一般的js区分），并且在引入的时候不能够省略后缀名，需要 



```
import CompA from 'compA/index.jsx'
```


不要省去后面的`/index.jsx`，否则会报错。

## 具体的规则含义都可以去ESlint中文网通过上方的搜索查询

http://eslint.cn/docs/user-guide/configuring


## ESLint关闭规则
有的文件不想因为一些eslint规则报错，可以通过注释来配置eslint规则是否开启：

"off" 或 0 - 关闭规则
"warn" 或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
"error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)

如：

```
/* eslint eqeqeq: "off" */
```

上面在该文件下关闭了eqeqeq 校验规则。



具体参考：
http://eslint.cn/docs/user-guide/configuring#configuring-rules

### webpack中接入eslint

可以使用
[eslint-loader](https://github.com/MoOx/eslint-loader)


## 编辑器ESLint插件配置

### 1. webstorm  ESLint 简单配置
点webstorm，Perferences 里搜索 eslint，配置ESLint package为项目本地node_modules下安装的eslint (不要去指定全局的，各个项目不一样的)


## 其他
可以安装和配置 [eslint-config-ali](https://www.npmjs.com/package/eslint-config-ali) 这是阿里巴巴的eslint配置规范，能让项目更系统和规范，里面也介绍了eslint提示在各个编辑器中的配置方法。





