# child_process

**执行系统命令（child_process.exec()），这个很常用，功能很强大。比如，用来执行curl命令。**

要curl一下天气的接口返回json格式的数据，可能我要对它进行一番操作，这里就打印出来不操作。

新建nodejs文件，名为cmd_exec.js:

```
var exec = require('child_process').exec; 
var cmdStr = 'curl http://www.weather.com.cn/data/sk/101010100.html';
exec(cmdStr, function(err,stdout,stderr){
    if(err) {
        console.log('get weather api error:'+stderr);
    } else {
        /*
        这个stdout的内容就是上面curl出来的这个东西：
        {"weatherinfo":{"city":"北京","cityid":"101010100","temp":"3","WD":"西北风","WS":"3级","SD":"23%","WSE":"3","time":"21:20","isRadar":"1","Radar":"JC_RADAR_AZ9010_JB","njd":"暂无实况","qy":"1019"}}
        */
        var data = JSON.parse(stdout);
        console.log(data);
    }
});
```

来感受一下直接curl出来和通过运行脚本的出来的结果是一样的。
