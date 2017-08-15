# git常用技能整理

## 优先参考官方的文档


## 新进入一个gitlab库需要增加ssh

### Clone
git clone gitUrl
（前端项目一般接下来先要npm install）

### 新建并切换到该分支


如果是从远程仓库拉取特定的分支：


如果是从某个分支上生成开发分支 dev/…
注意本地需要新建立一个分支比如 dev 然后从dev上去push到 origin的dev/…上

### 
必须先切换分支到master

再pull远端代码到当前分支上

（pull完之后也需要在npm install一下，使用tnpm下载和更新模块回更快，链接http://web.npm.alibaba-inc.com/）

之前clone的代码无论是主分支还是某个分支只需要


相当于 git fetch + git merge

### 从指定分支拉取代码到本地指定分支


### 



git branch --set-upstream-to=origin/someBranch daily/0.0.30

### 分支重命名
本地分支
git branch -m oldname newname

### 提交代码
提交之前先要切回master分支  git pull一下 (必须切到master下pull然后切到自己的分支上merge master之后再build，再git status(build下不一样可以git add .) 再 push)

要合并哪个分支的代码，必须切到该分支下 去 pull

然后回到要发布的目录： git merge master   (把master目录合并到当前目录)

## 日常发布
功能在本地开发好之后，就可以通过如下命令进行编译，提交到日常了：
... build

git add .   （git发明了一个叫做暂存区的概念，conmit之前要add一下）

git commit -m 'dev'  （提交当前工作空间的修改内容提交的时候必须用-m来输入一条提交信息，如’dev’）

git push origin daily/x.x.x:daily/x.x.x   (git push：将本地commit的代码更新到远程版本库中，例如'git push origin b1:b2'就会将本地名为b1的代码更新到名为b2的远程版本库中, 第一次写daily/x.x.x:daily/x.x.x，以后只需要写一个，否则会覆盖远程分支)

## 发布至线上
开发分支在日常测试完成之后发布至线上：
git tag publish/x.x.x
git push origin publish/x.x.x:publish/x.x.x

一般提交前先pull再build

git push到远程日常时，第一次写daily/x.x.x:daily/x.x.x，以后只需要写一个，否则会覆盖远程分支

### git stash（存储目前状态，可不提交后切换分支）
你不想提交进行了一半的工作，否则以后你无法回到这个工作点。解决这个问题的办法就是git stash命令。

再切回原来分支，git stash pop回到上次stash前，也就是修改了的最后状态


### 强制提交代码到远程分支（如果冲突以本地代码为准，只适用于分支是自己一人用的情况）



### 自己已经发布的版本更新到远端
需要先指定本地分支提交和更新的远程代码分支：


如：


然后就只需要 git push origin daily/x.x.x（远程仓库的号） 就行了   
如果 后面在跟一个分支的话，就是把当前目录的分支创建并作为远端的后者分支， 后面那个分支如果之前存在回删掉覆盖



git commit -am "<message>"，将所有修改，但未进stage的改动加入stage，并记录commit信息。(某种程度上相当于git add和git commit -m的组合技

目前还是用 git add . + git commit –m ‘’

### 冲突解决
如果出现冲突，要找到位置之后再app目录下 上面的是自己的分支，下面是要提交的分支，把上面的内容加到下面之后只保留下面（master）的,，

然后 

git commit –m ‘dev’
（如果冲突时是无关紧要的构建文件的话可以 git add . 然后 git commit –m ‘dev’  之后点：wq之后再git merge 主分支）

再git push

参考：

### MERGE_MSG.swp" already exists问题
Swap file ".git/.MERGE_MSG.swp" already exists!

解决方法：


git commit -m "";git push master 之后，再执行 git merge branchName 就好啦

### 




```
git fetch --all  
git reset --hard origin/master
```



### git 分支后面的 数字意思 

+a ~b –c 代表相比远程分支 增加a 修改b 删除c个文件，需要 git status 查看具体信息




http://wlog.cn/soft/git-quick-start.html

### 仓库地址如果变化，修改本地代码提交的远程仓库



### 回滚
git reset –hard



#### 

http://www.cnblogs.com/qualitysong/archive/2012/11/27/2791486.html

http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000

### 打tag和删除tag

列显已有的标签


#### 删除本地tag

比如tag是v1.0.0

git tag -d v1.0.0

#### 删除远程tag

git push origin :refs/tags/v1.0.0

