## 其他数据类型类
### 1. 对特定的数据类型进行特定操作前，必须先检查其是否存在与数据类型是否正确（可以用typeof），如：回调函数执行前先检查其是否为函数：

```
//react代码

const {onClickCallback} = this.props;

// 只有当回调函数存在切类型为函数时，才去执行回调函数，避免传过来的值类型不对而导致js报错
if(onClickCallback && typeof onClickCallback === 'function'){
  onClickCallback();
}
```

