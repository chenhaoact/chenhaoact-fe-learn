# git常用技能整理

## 优先参考官方的文档
https://git-scm.com/book/zh/v2

## 新进入一个gitlab库需要增加ssh

### Clone
git clone gitUrl
（前端项目一般接下来先要npm install）

### 新建并切换到该分支
git checkout -b 分支名如daily/0.0.1

如果是从远程仓库拉取特定的分支：
git clone -b 远程分支名 <remote_repo> 

如果是从某个分支上生成开发分支 dev/…
注意本地需要新建立一个分支比如 dev 然后从dev上去push到 origin的dev/…上不要直接在dailly/… 下写然后push到 dev/. 上

### master上pull（从远端更新）最新代码
必须先切换分支到master
git checkout master
再pull远端代码到当前分支上
git pull gitUrl
（pull完之后也需要在npm install一下，使用tnpm下载和更新模块回更快，链接http://web.npm.alibaba-inc.com/）

之前clone的代码无论是主分支还是某个分支只需要
git pull  
(有更改每天都pull一下，保持所拉取的代码为最新)
相当于 git fetch + git merge

### 从指定分支拉取代码到本地指定分支（常用！）


```
git pull origin 远程分支:本地某分支
```



### 指定本地分支提交和更新的远程代码分支：

(特别是本地分支有多人合作开发，要从远程某分支先pull，那么必须先指定upstream，否则git bash里会显示不了文字，其实没有pull,也引文落后于远程分支而不能push,建议git bash出现空行的时候，换个命令行工具)

git branch --set-upstream-to=origin/someBranch daily/0.0.30

### 分支重命名
本地分支
git branch -m oldname newname

### 提交代码（需要先合并master）
提交之前先要切回master分支  git pull一下 (必须切到master下pull然后切到自己的分支上merge master之后再build，再git status(build下不一样可以git add .) 再 push)

要合并哪个分支的代码，必须切到该分支下 去 pull

然后回到要发布的目录： git merge master   (把master目录合并到当前目录)


**如果merge master时遇到**：

fatal: refusing to merge unrelated histories

是不同项目历史的原因，在当前分枝下执行：

```
git pull origin master --allow-unrelated-histories
```

具体原因参考：http://blog.csdn.net/lindexi_gd/article/details/52554159


## 日常发布
功能在本地开发好之后，就可以通过如下命令进行编译，提交到日常了： 
... build

git add .   （git发明了一个叫做暂存区的概念，conmit之前要add一下）            （如果删除过某文件 还要执行git rm 文件路径）   

git commit -m 'dev'  （提交当前工作空间的修改内容提交的时候必须用-m来输入一条提交信息，如’dev’）（在push之前先切换到master版本 git pull一下，如果有更新就切回分支把master合并过来，分析清楚冲突之后再 push）  

git push origin daily/x.x.x:daily/x.x.x   (git push：将本地commit的代码更新到远程版本库中，例如'git push origin b1:b2'就会将本地名为b1的代码更新到名为b2的远程版本库中, 第一次写daily/x.x.x:daily/x.x.x，以后只需要写一个，否则会覆盖远程分支)

## 发布至线上
开发分支在日常测试完成之后发布至线上：  
git tag publish/x.x.x  
git push origin publish/x.x.x:publish/x.x.x

一般提交前先pull再build

git push到远程日常时，第一次写daily/x.x.x:daily/x.x.x，以后只需要写一个，否则会覆盖远程分支

### git stash（存储目前状态，可不提交后切换分支）
你不想提交进行了一半的工作，否则以后你无法回到这个工作点。解决这个问题的办法就是git stash命令。
“‘储藏”“可以获取你工作目录的中间状态切换到另一分支，pull,
再切回原来分支，git stash pop回到上次stash前，也就是修改了的最后状态Merge 刚才pull的分支
https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%82%A8%E8%97%8F%EF%BC%88Stashing%EF%BC%89

### 强制提交代码到远程分支（如果冲突以本地代码为准，只适用于分支是自己一人用的情况）

git push origin HEAD --force

### 自己已经发布的版本更新到远端
需要先指定本地分支提交和更新的远程代码分支：
git branch --set-upstream-to=origin/someBranch daily/0.0.30

如：
git branch --set-upstream-to=origin/daily/0.1.3 daily/0.1.3

然后就只需要 git push origin daily/x.x.x（远程仓库的号） 就行了   
如果 后面在跟一个分支的话，就是把当前目录的分支创建并作为远端的后者分支， 后面那个分支如果之前存在回删掉覆盖

### git commit –am  

git commit -am "<message>"，将所有修改，但未进stage的改动加入stage，并记录commit信息。

**(某种程度上git commit –am 相当于git add和git commit -m的组合技，建议使用此命令来提交)**

**注意：
如果出现nothing added to commit but untracked files present (use "git add" to track)

用git add .  + git commit -m '' 可以解决**

### 冲突解决
如果出现冲突，要找到位置之后再app目录下 上面的是自己的分支，下面是要提交的分支，把上面的内容加到下面之后只保留下面（master）的,，

然后 Git merge 之后（git status没有问题之后） 

git commit –m ‘dev’
（如果冲突时是无关紧要的构建文件的话可以 git add . 然后 git commit –m ‘dev’  之后点：wq之后再git merge 主分支）

再git push

参考：http://www.cnblogs.com/sinojelly/archive/2011/08/07/2130172.html

### MERGE_MSG.swp" already exists问题
Swap file ".git/.MERGE_MSG.swp" already exists![O]pen Read-Only, (E)dit anyway, (R)ecover, (Q)uit, (A)born:

解决方法：

找到".git/.MERGE_MSG.swp"，之后删除即可，然后重新git add .;
git commit -m "";git push master 之后，再执行 git merge branchName 就好啦

### Git pull强制覆盖掉本地文件（常用！）

如强行本地master分支与远程master一致



```
git fetch --all  
git reset --hard origin/master
```



### git 分支后面的 数字意思  

+a ~b –c 代表相比远程分支 增加a 修改b 删除c个文件，需要 git status 查看具体信息

Git参考
http://www.cnblogs.com/eddy-he/archive/2012/03/29/branch.html

http://wlog.cn/soft/git-quick-start.html

### 仓库地址如果变化，修改本地代码提交的远程仓库

git remote set-url origin

### 回滚
git reset –hard  //回滚到 merge 前的版本，回滚一版

git reset --hard HEAD~2   // 取消当前版本之前的两次提交

#### git代码库回滚参考

http://www.cnblogs.com/qualitysong/archive/2012/11/27/2791486.html

http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000

## 删除

### 删除分枝


```
git branch -D 分枝名
```

(-d 只有在合并完成后才能删除， -D 则是强制删除)

### 打tag和删除tag

列显已有的标签
列出现有标签的命令非常简单，直接运行 git tag 即可

#### 删除本地tag

比如tag是v1.0.0

git tag -d v1.0.0

#### 删除远程tag

git push origin :refs/tags/v1.0.0


