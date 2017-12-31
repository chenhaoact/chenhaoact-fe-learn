

# github使用技巧

## 一 用好Github来阅读项目源代码
### 通过某分枝的Commit记录看整个项目分枝的提交记录
项目切刀某分枝在首页可以看到该分支项目总的提交更新历史，查看这里可以理清楚项目从0到1是如何搭建和迭代的，对阅读了理解源码很有帮助。（**建议这样通过Commit记录从项目0点开始看项目的搭建来阅读源码，而不是一下子就看目前最新的代码是怎样的，代码量太大没有先后时间顺序，看起来会比较乱**）

### 通过History查看某个文件所有的修改记录
github打开每个文件的详情页，在**右上角有该文件的History，点击可以看到这个文件所有的修改记录**，通过此功能可以追踪到某个文件的历史，方便定位该文件提交中的作用以及定位bug。

## 二 发现github热门项目
点击头像下拉菜单里的explore或进入下列链接
https://github.com/explore

可以看到本周或本月github热门项目（某时间段star最多）

**也可以通过以下平台寻找热门项目：**
https://www.ctolib.com/
https://libraries.io/
https://juejin.im/repos

###  搜某个主题标签的库

每个仓库是可以贴标签的，在github的搜索框里搜某个主题标签的库（如下所示搜了带javascript便签的），然后按most stars排序可以有助于发现一些流行受关注的代码仓库

topic:javascript


## 三 获取github项目的star数和star等按钮 （常用）

参考：
获取github项目的star数和star等按钮
https://github.com/mdo/github-buttons

获取斜着的fork me on Github 的标签
https://github.com/blog/273-github-ribbons

更多的api可以看 github 官方的api（点击Learn more about vN of the GitHub API）
https://developer.github.com/

**google或百度搜索github star api** 就可以找到上述需要的答案。




## 四 GitHub 上参与开源项目贡献

### 重点！找到可以贡献代码点的技巧
1. 在源代码中搜索 TODO:
经常会有一些TODO:的任务可以去完成，自己实现测试没问题就可以提交上去

2. 在项目的issue中找使用者提出的一些问题，自己去解决然后提交，修复


### 1. Fork
项目右上角点击Fork。

相当于在原项目的主分支上又建立了一个分支，你可以在该分支上任意修改，如果想将你的修改合并到原项目中时，可以pull request，这样原项目的作者就可以将你修改的东西合并到原项目的主分支上去。

### 2. Clone

从自己github仓库git clone自己fork的项目到本地：

如：


```
git clone https://github.com/chenhaoact/react.git

```


### 3. 保持同步

先在本地项目中，运行 

```
git remote add upstream 官方项目仓库.git
```

将原项目作为了本地项目的上游。

**（1）长期参与同步方法（推荐）：**

执行上面git remote命令后，再执行：

```
 git remote -v  //用来观察改动

```


同步原项目的改动，执行

```
  git fetch upstream 

```

这会将原项目所有分支的改动都存储在本地。

原项目 master 分支会存为 upstream/master


再执行：

```
git branch --set-upstream-to=upstream/master master

```

**这样每次当上游 master 有改动后，只需在本地 master 分支 git pull 即可。然后再在自己的dev分枝上合并自己的master即可更新。**

同理可以按需要处理 develop 分支等。

### 4. 开发分枝
借鉴 Git Flow 的流程。在 master 外，建立一个 develop 分支用于开发，而且，每一个新特性的开发都会从 develop 分支创建新分支，新特性开发完成后再合并到 develop 分支。


### 5. pull request



参考：

在 GitHub 上贡献开源项目的一般步骤
[https://github.com/nixzhu/dev-blog/blob/master/2016-02-17-contribute-on-github.md](https://github.com/nixzhu/dev-blog/blob/master/2016-02-17-contribute-on-github.md)

如何参与一个GitHub 开源项目
[http://www.cnblogs.com/lanxuezaipiao/p/3662328.html
](http://www.cnblogs.com/lanxuezaipiao/p/3662328.html)

如何给开源项目贡献代码
[https://gist.github.com/zxhfighter/62847a087a2a8031fbdf
](https://gist.github.com/zxhfighter/62847a087a2a8031fbdf)

如何用好 github 中的 watch、star、fork
http://www.jianshu.com/p/6c366b53ea41












