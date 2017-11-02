## 数组类

### 1. 数组下标从 0 开始 到length-1 不是到length


如：检查时间段列表上下周是否可点击的代码
```
//点击切换下周的按钮里的代码
const {selected,weekList} = this.state

//注意这里都是用的weekList.length -1去做判断和限界
let selectedToChange = selected + 1 <= weekList.length -1 ? selected + 1 : weekList.length -1;

//用>=  和 weekList.length - 1 做比较
const nextWeekActiveToChange = selectedToChange >= weekList.length - 1 ? false :true

weekList[nextWeekActiveToChange] ...

```

### 2. 对从后端拿到的数组，对象等数据进行操作时首先要保证是有值且类型正确，否则有时候后端不给，前端就会因异常而出现故障

最常见的方法时前端 || 一个默认值，如：



```
let array1 = json.data.list || []; //即使从后端拿不到数据，也能保证它是一个数组数据，从而让对数组的操作不保错

```




