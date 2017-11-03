# eslint使用实践

## React项目接入ESLint

安装并配置 [eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)

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

## 其他
可以安装和配置 [eslint-config-ali](https://www.npmjs.com/package/eslint-config-ali) 这是阿里巴巴的eslint配置规范，能让项目更系统和规范，里面也介绍了eslint提示在各个编辑器中的配置方法。



