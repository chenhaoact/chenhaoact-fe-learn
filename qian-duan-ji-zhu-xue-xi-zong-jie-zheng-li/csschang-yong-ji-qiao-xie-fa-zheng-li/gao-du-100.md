# 高度100%

如要父容器的高度就撑满，所有需要**从最外层就开始一直设置height:100%**，连续继承下来才行。

另外父容器的告诉占满100%后，**子容器position:relative再设置height:100%可能不起作用，改成position:absolute可以起作用**。

## 参考
如何让 height:100%; 起作用
http://www.webhek.com/post/css-100-percent-height.html