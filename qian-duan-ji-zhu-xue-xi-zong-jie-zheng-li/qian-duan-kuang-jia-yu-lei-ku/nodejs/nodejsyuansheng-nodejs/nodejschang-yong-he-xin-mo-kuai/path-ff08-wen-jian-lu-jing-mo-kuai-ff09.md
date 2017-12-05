# path （文件路径模块）

## 一 属性
TODO

## 二 方法
### 1. path.join() 连接路径
语法：


```
path.join([path1][, path2][, ...])
```


用于连接路径。该方法的主要用途在于，会正确使用当前系统的路径分隔符，Unix系统是"/"，Windows系统是"\"。

例子：

```
var path = require('path');
path.join(mydir, "foo");

上面代码在Unix系统下，会返回路径mydir/foo。
```


### 2. path.resolve() 将相对路径转为绝对路径
语法：
path.resolve([from ...], to)
将 to 参数解析为绝对路径。

```
path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif')
// 如果当前目录是/home/myself/node，返回/home/myself/node/wwwroot/static_files/gif/image.gif
```

例子：

```
path.resolve('src/index') // 返回的是当前项目根目录下src/index的系统绝对路径
path.resolve() //返回的是当前node脚本/命令执行做在的文件夹绝对路径
```



### 3. accessSync() 同步读取一个路径
语法：

例子：




### 4. path.relative()
接受两个参数，这两个参数都应该是绝对路径。该方法返回第二个路径相对于第一个路径的那个相对路径。
语法：


```
path.relative(from, to)

```

例子：





### 5. path.parse() 返回路径各部分的信息。
语法：
path.parse(pathString)
返回路径字符串的对象。

例子：


```
var myFilePath = '/someDir/someFile.json';
path.parse(myFilePath).base
// "someFile.json"
path.parse(myFilePath).name
// "someFile"
path.parse(myFilePath).ext
// ".json"
```




其他相关方法有：

path.dirname(p)
返回路径中代表文件夹的部分，同 Unix 的dirname 命令类似。

path.basename(p[, ext])
返回路径中的最后一部分。同 Unix 命令 bashname 类似。

path.extname(p)
返回路径中文件的后缀名，即路径中最后一个'.'之后的部分。如果一个路径中并不包含'.'或该路径只包含一个'.' 且这个'.'为路径的第一个字符，则此命令返回空字符串。



## 参考
### 已学习
《JavaScript 标准参考教程（alpha）Node.js Path模块》
http://javascript.ruanyifeng.com/nodejs/path.html

Node.js Path 模块-菜鸟教程
http://www.runoob.com/nodejs/nodejs-path-module.html

### 待学习