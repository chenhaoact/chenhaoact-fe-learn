# n与nvm-node版本控制与切换

**个人建议使用nvm**，首先，n 对全局模块毫无作为，因此有可能在切换了 node 版本后发生全局模块执行出错的问题；nvm 的全局模块存在于各自版本的沙箱中，切换版本后需要重新安装，不同版本间也不存在任何冲突。

另外，n项目目前14年之后tj已经不维护了，整个项目活跃度比较低，而nvm无论从活跃度,维护程度还是项目的关注数上都远超n，所以使用nvm更稳定一些。

## 安装nvm
### Mac下
安装执行gitHub上的命令

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
```

确认是否安装好：



```
command -v nvm
```

如果上述命令返回nvm，则说明安装好了。

**注意：如果没有安装好，按照官网的说明**（Note: On OS X, if you get nvm: command not found after running the install script, one of the following might be the reason）一般是因为：
系统没有.bash_profile文件，

注意**先在命令行工具中打开一个新的窗口(新的命令窗口也会影响到安装是否成功)**

再执行 `touch ~/.bash_profile`

在执行上述安装的命令，

再在新的命令行中输 `nvm: command not found`

返回nvm，则说明安装成功。


## 三 使用nvm

### 1. 安装某个特定版本的nodejs


```
nvm install 4.6.0
```

nvm install stable 安装node速度很慢，可以通过配置淘宝npm镜像来加快nvm安装node的速度：
建议把下列内容加入到 .bash_profile 文件中:



```
# nvm
export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node

```

然后nvm按照node就会很快。

### 2. 切换成某个特定版本的nodejs

```
nvm use v4.6.0
```

node版本就切换到了4.6.0

如果node -v没有变，需要新打开一个命令行窗口执行命令（因为命令行窗口的bash有缓存，bash改变后需要在新开的命令行窗口中才能生效）

### 3. 列出当前所有的node版本

```
nvm ls
```

### 4. 设置默认 node 版本

每次打开终端后，都自动设置成指定版本

```
nvm alias default 0.12.7 #设置默认 node 版本为 0.12.7

```


## 参考
nvm
https://github.com/creationix/nvm

### 教程
正确的安装和使用nvm(mac)
http://www.imooc.com/article/14617

使用 nvm 让不同版本的 Node.js 共存
https://juejin.im/entry/5705f95671cfe40054248f16

管理 node 版本，选择 nvm 还是 n？
http://taobaofed.org/blog/2015/11/17/nvm-or-n/

node版本管理 n和nvm说明
https://hao5743.github.io/2017/02/24/node%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86%20n%E5%92%8Cnvm%E8%AF%B4%E6%98%8E/

使用 nvm 管理不同版本的 node 与 npm
http://www.cnblogs.com/kaiye/p/4937191.html
