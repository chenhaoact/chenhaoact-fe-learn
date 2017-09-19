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

## 对象类

### 对象赋值不要用 = ，用 = 相当于是给了引用，最后修改的时候还会修改原对象，造成污染，可以用 es6的 Object.assign() 去赋值对象值到新的对象里：


```
//let itemToChange = item; item是对象时，错

let itemToChange = Object.assign({},item);
itemToChange.a = 'a';

```







