# ES6 字符串新特性

## 一 模板字符串

### 简介
TODO

### 应用

#### （1）在React中给className添加多个（可以带变量的）样式类

不依赖classname库，也能通过模板字符串轻松实现此功能：

```
const disabledCls = this.state.btnDisabled ? 'disabled' : '';
const cls = `submit-btn ${disabledCls}`;

return (
  <Button className={cls}></Button>
);
```

