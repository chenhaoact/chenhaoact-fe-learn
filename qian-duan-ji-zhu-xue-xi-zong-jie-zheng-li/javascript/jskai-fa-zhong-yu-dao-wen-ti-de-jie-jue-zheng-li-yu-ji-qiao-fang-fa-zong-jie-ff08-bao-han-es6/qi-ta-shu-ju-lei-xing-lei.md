## 其他数据类型类
### 1. 对特定的数据类型进行特定操作前，必须先检查其是否存在与数据类型是否正确（可以用typeof），

如：

#### （1）回调函数执行前先检查其是否为函数：

```
//react代码

const {onClickCallback} = this.props;

// 只有当回调函数存在切类型为函数时，才去执行回调函数，避免传过来的值类型不对而导致js报错
if(onClickCallback && typeof onClickCallback === 'function'){
  onClickCallback();
}
```

#### (2)执行 .map（） 先判断数据是否是array（否则有时从后端拿到的数据不是数组或者没拿到就直接执行map()等遍历操作会直接抛错导致页面白屏故障！）:

```
// 使用了lodash的_.isArray
_.isArray(data.list) ?data.list.map((item)={ ... }) : ''
```



