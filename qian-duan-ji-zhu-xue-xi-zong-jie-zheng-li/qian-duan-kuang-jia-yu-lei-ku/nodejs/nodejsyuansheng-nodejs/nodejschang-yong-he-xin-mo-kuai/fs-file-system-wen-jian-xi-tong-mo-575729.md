# fs (File System 文件系统模块)
## 一 简介
fs是filesystem的缩写，该模块提供本地文件的读写能力，基本上是UNIX（POSIX）标准的文件操作API的简单包装。

### 异步与同步
fs模块几乎对所有操作提供异步和同步两种操作方式，供开发者选择。

例如读取文件内容有异步的 fs.readFile() 和同步的 fs.readFileSync()。

异步的方法最后一个参数为回调函数，回调函数的第一个参数包含了错误信息(error)。

**建议用异步方法**，比起同步，异步方法**性能更高，速度更快，而且没有阻塞。**

## 二 使用

**注：下列只列出推荐使用的异步方法，后面加Sync即是同步方法。**

### 1.打开文件

异步模式下打开文件的语法：
```
fs.open(path, flags[, mode], callback)

```

参数：
path - 文件的路径**（注意这里文件的文件名必须和文件里保持一致，比如名为act-init的文件虽然默认会当成txt文件处理，但是文件名是act-init没有.txt就不能去加.txt后缀），具体的文件路径时相对于当前的js而言的**。
flags - 文件打开的行为。具体值详见下文。
mode - 设置文件模式(权限)，文件创建默认权限为 0666(可读，可写)。
callback - 回调函数，带有两个参数如：callback(err, fd)。

flags 参数可以是以下值：
r 读取模式
w 写入模式
a 追加模式打开文件，如文件不存在会创建。
上面三种还可以和（s（同步） +（可写）  x（） ）互相组合。具体查阅教程：http://www.runoob.com/nodejs/nodejs-fs.html

例子：

打开 a.txt 文件（可读写）:

```
var fs = require("fs");

// 异步打开文件
console.log("准备打开文件！");
fs.open('a.txt', 'r+', function(err, fd) {
   if (err) {
       return console.error(err);
   }
  console.log("文件打开成功！");     
});
```

执行结果：


```
$ node file.js
 
准备打开文件！
文件打开成功！
```

### 2.获取文件信息 
通过异步模式获取文件信息的语法：

```
fs.stat(path, callback)
```

参数：
path - 文件路径。
callback - 回调函数，带有两个参数如：(err, stats), stats 是 fs.Stats 对象。

**fs.stat(path)执行后，会将stats类的实例返回给其回调函数。可以通过stats类中的提供方法判断文件的相关属性**。

stats类的方法有：isFile()	 isDirectory() isSocket等。

例子：


```
var fs = require("fs");

console.log("准备打开文件！");
fs.stat('a.txt', function (err, stats) {
   if (err) {
       return console.error(err);
   }
   console.log(stats); //打印出文件信息对象
   console.log("读取文件信息成功！");
   
   // 检测文件类型
   console.log("是否为文件(isFile) ? " + stats.isFile());
   console.log("是否为目录(isDirectory) ? " + stats.isDirectory());    
});
```

执行结果：


```
$ node file.js 

准备打开文件！
{ dev: 16777220,
  mode: 33188,
  nlink: 1,
  uid: 501,
  gid: 20,
  rdev: 0,
  blksize: 4096,
  ino: 40333161,
  size: 61,
  blocks: 8,
  atime: Mon Sep 07 2015 17:43:55 GMT+0800 (CST),
  mtime: Mon Sep 07 2015 17:22:35 GMT+0800 (CST),
  ctime: Mon Sep 07 2015 17:22:35 GMT+0800 (CST) }
读取文件信息成功！
是否为文件(isFile) ? true
是否为目录(isDirectory) ? false
```

### 3.读取文件
异步模式下读取文件的语法：

```
fs.read(fd, buffer, offset, length, position, callback)
```

参数：
fd - 通过 fs.open() 方法返回的文件描述变量。
buffer - 数据写入的缓冲区。
offset - 缓冲区写入的写入偏移量。
length - 要从文件中读取的字节数。
position - 文件读取的起始位置，如果 position 的值为 null，则会从当前文件指针的位置读取。
callback - 回调函数，有三个参数err, bytesRead, buffer，err 为错误信息， bytesRead 表示读取的字节数，buffer 为缓冲区对象。

例子：
a.txt 文件内容为：
hi

创建 file.js 文件：


```
var fs = require("fs");
var buf = new Buffer(1024);

console.log("准备打开已存在的文件！");
fs.open('input.txt', 'r+', function(err, fd) {
   if (err) {
       return console.error(err);
   }
   console.log("文件打开成功！");
   console.log("准备读取文件：");
   fs.read(fd, buf, 0, buf.length, 0, function(err, bytes){
      if (err){
         console.log(err);
      }
      console.log(bytes + "  字节被读取");
      
      // 仅输出读取的字节
      if(bytes > 0){
         console.log(buf.slice(0, bytes).toString());
      }
   });
});
```


执行结果：


```
$ node file.js 

准备打开已存在的文件！
文件打开成功！
准备读取文件：
3  字节被读取
hi
```




### 4.写入文件
异步模式下写入文件的语法：


```
fs.writeFile(file, data[, options], callback)
```

如文件存在，该方法写入内容会覆盖原文件内容。

参数：
file - 文件名或文件描述符。
data - 要**写入文件的数据，可以是 String(字符串) 或 Buffer(流) 对象**。
options - 该参数是一个对象，包含 {encoding, mode, flag}。默认编码为 utf8, 模式为 0666 ， flag 为 'w'
callback - 回调函数，回调函数只包含错误信息参数(err)，在写入失败时返回。

例子：
将字符串写入某文件，并读取其内容：


```
var fs = require("fs");

console.log("准备写入文件");
fs.writeFile('input.txt', '我是通过写入的文件内容！',  function(err) {
   if (err) {
       return console.error(err);
   }
   console.log("数据写入成功！");
   console.log("--------我是分割线-------------")
   console.log("读取写入的数据！");
   fs.readFile('input.txt', function (err, data) {
      if (err) {
         return console.error(err);
      }
      console.log("异步读取文件数据: " + data.toString());
   });
});
```

执行结果：


```
$ node file.js 

准备写入文件
数据写入成功！
--------我是分割线-------------
读取写入的数据！
异步读取文件数据: 我是通过写入的文件内容
```




## 参考
官方api
https://nodejs.org/api/fs.html

### 教程
### 已学习
Node.js 文件系统（菜鸟教程）
http://www.runoob.com/nodejs/nodejs-fs.html

### 待学习
《JavaScript 标准参考教程（alpha）草案二：Node.js fs模块》，阮一峰
http://javascript.ruanyifeng.com/nodejs/fs.html



