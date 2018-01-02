# pm2-比forever更强大而且支持可视化界面监控管理

云服务器上运行node应用：

来使用的是forever让nodejs应用后台执行：

后来改成了**更强大的pm2，和forever相比pm2有更多的支持，而且还支持可视化界面监控和管理**，详细可以参考：

告别node-forever,拥抱PM2：

[http://www.oschina.net/translate/goodbye-node-forever-hello-pm2?cmp](http://www.oschina.net/translate/goodbye-node-forever-hello-pm2?cmp)

pm2官方项目与文档：

[https://github.com/Unitech/pm2](https://github.com/Unitech/pm2)

[http://pm2.keymetrics.io/](http://pm2.keymetrics.io/)

教程：

PM2 介绍：

[https://www.douban.com/note/314200231/](https://www.douban.com/note/314200231/)



## 使用:

每次代码更新传到服务器后，在服务器命令行中使用命令（任何路径都可以，pm2会取服务器下所有的node服务）：


```
pm2 reload all         

```


进行0秒停机重载进程 \(用于 NETWORKED 进程\)

注意：
**如果只是静态资源变了，node代码没变的话，是不需要重启服务的**。只用上传打包的静态资源到服务器对应位置即可生效。

### 其他常用命令


```
pm2 list      # 显示所有进程状态
```



