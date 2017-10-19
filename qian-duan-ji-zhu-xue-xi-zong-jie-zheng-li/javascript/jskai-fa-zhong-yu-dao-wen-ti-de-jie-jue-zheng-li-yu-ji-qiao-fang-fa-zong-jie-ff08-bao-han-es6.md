# js问题及故障的解决与技巧方法整理（包含es6）

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




## 对象类

### 对象赋值不要用 = ，用 = 相当于是给了引用，最后修改的时候还会修改原对象，造成污染，可以用 es6的 Object.assign() 去赋值对象值到新的对象里：

```
//let itemToChange = item; item是对象时，错，改变itemToChange时会改动原来的item

let itemToChange = Object.assign({},item);
itemToChange.a = 'a';
```







