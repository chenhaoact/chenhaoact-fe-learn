## 项目发布注意事项

### 数据接口异常的处理必须考虑和兼容
上线前必须自测和处理到，稳定性保障，**所有接口挂了或接口data完全不返回数据，页面也要正常的展示空数据的状态，且 及时提示出异常，不能出现接口挂了就一直loading的状态，不能出现因为js抛异常就让页面无法再操作。 ** 

**记住：**
**任何时候页面不能出现白屏或一直loadding卡死**，即使是异常，也应该有提示的页面展示。

### 代码发布前的review
另外代码上线发布前必须找人review, 用webstorm git对比或者gitlab/github的pull request对比功能重过修改过的每一行代码，避免因为不小心手误删改代码导致的故障，多一个人把关会更保险一些。

## 常见的前端代码引发的故障及防范写法

见：

[重！js问题及故障的解决与技巧方法整理（包含es6）](/qian-duan-ji-zhu-xue-xi-zong-jie-zheng-li/javascript/jskai-fa-zhong-yu-dao-wen-ti-de-jie-jue-zheng-li-yu-ji-qiao-fang-fa-zong-jie-ff08-bao-han-es6.md)