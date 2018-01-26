# 提升开发效率与工程质量的技巧

**好的工具就相当于是各种先进的武器，只要能提高项目开发的效率和质量，就要多学习去用。**

**注意：建议开发项目时把webstorm和vscode都打开，需要用到那个编辑器的特定功能，就切到那个编辑器，取长补短**，这样可以最大程度上发挥两个编辑器优势，把工具带来的开发效率和质量提升到极致。

### 1. 常用的设置 settings
点击顶栏code -> 首选项 -> 设置，进入settings.json 。

#### 设置文件自动保存 （vscode默认不自动保存文件，修改后每次手动保存很麻烦）

比如设置文件自动保存：


settings.json：
```
{
  files.autoSave: onFocusChange   //焦点移出编辑器后就会自动保存
}
```

或者**直接打开编辑器系统顶栏的 文件-> 点击自动保存，即可设置成功**。



参考：
Visual Studio Code入门(译)
http://www.jianshu.com/p/3dda4756eca5


### 2. Snippets 定义常用代码块和自动补全（强烈推荐）

插件里面搜索Snippets，就会出来一大堆插件，最上面的是下载书最多的，挑选自己需要的，按照介绍使用即可，比如：React Snippets，Html Snippets，ES6 Snippets等。

参考：
向 VSC 添加代码段(Adding Snippets to Visual Studio Code)
https://jeasonstudio.gitbooks.io/vscode-cn-doc/content/md/%E5%AE%9A%E5%88%B6%E5%8C%96/%E7%94%A8%E6%88%B7%E5%AE%9A%E4%B9%89%E4%BB%A3%E7%A0%81%E6%AE%B5.html

[VS Code]跟我一起在Visual Studio Code 添加自定义snippet（代码段），附详细配置
http://blog.csdn.net/maokelong95/article/details/54379046



