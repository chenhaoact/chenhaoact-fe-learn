# 页面远程调试与演示

## 一 移动端页面调试
1. 本地npm run start启动服务（在npm run start 命令定义时的 webpack-dev-server命令 后面加 --host 0.0.0.0，这样在启动服务的时候回让本地资源可以通过ip访问）
2. Mac 在终端执行ipconfig getifaddr en0命令，查到本机ip。
3. 用 本地ip:本地服务端口/页面后面地址在移动端浏览器中访问即可。