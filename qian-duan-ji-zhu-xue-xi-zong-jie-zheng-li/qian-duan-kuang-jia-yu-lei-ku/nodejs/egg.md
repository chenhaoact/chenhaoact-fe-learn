# Egg.js
Egg.js 为企业级框架和应用而生，蚂蚁金服出品。

### 特点
Egg 的插件机制有很高的可扩展性，一个插件只做一件事。
奉行『约定优于配置』，按照一套统一的约定进行应用开发
提供基于 Egg 定制上层框架的能力
高度可扩展的插件机制
内置多进程管理
基于 Koa 开发，性能优异
框架稳定，测试覆盖率高
渐进式开发

### 与社区框架的差异

**Express** 是 Node.js 社区广泛使用的框架，简单且扩展性强，适合做个人项目。但框架**本身缺少约定，标准的 MVC 模型会有各种千奇百怪的写法**。Egg 按照约定进行开发，奉行『约定优于配置』，团队协作成本低。

Sails 是和 Egg 一样奉行『约定优于配置』的框架，扩展性也非常好。但是相比 Egg，**Sails 支持 Blueprint REST API、WaterLine 这样可扩展的 ORM、前端集成、WebSocket 等，但这些功能都是由 Sails 提供**的。**而 Egg 不直接提供功能，只是集成各种功能插件**，比如实现 egg-blueprint，egg-waterline 等这样的插件，再使用 sails-egg 框架整合这些插件就可以替代 Sails 了。



## 


## 参考
https://github.com/eggjs/egg

https://eggjs.org/

