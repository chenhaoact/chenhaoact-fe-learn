# js开发中遇到问题及bug的解决整理与技巧方法总结（包含es6）

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



