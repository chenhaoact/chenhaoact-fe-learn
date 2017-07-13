#HTTPS

##什么是HTTPS?

 HTTPS 协议（学名 TLS 协议）。
 
不使用SSL/TLS（HTTPS）的HTTP通信，就是不加密的通信。所有信息明文传播，有三大风险：
（1） 窃听风险
（2） 篡改风险
（3） 冒充风险

**SSL/TLS协议是为了解决这三大风险而设计**，希望能：
（1） **所有信息加密传播，第三方无法窃听**。
（2） **有校验机制，一旦篡改，通信双方立刻发现**。
（3） **配备身份证书**，防止身份被冒充。

参考：
[HTTPS 协议概述
](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)

[HTTPS的七个误解（译文）
](http://www.ruanyifeng.com/blog/2011/02/seven_myths_about_https.html)

##HTTPS升级
为了升级到 HTTP/2 协议，必须先启用 HTTPS。

参考：
[HTTPS 升级指南](http://www.ruanyifeng.com/blog/2016/08/http.html)