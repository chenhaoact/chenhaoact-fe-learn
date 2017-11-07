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

### 3. 数组的浅拷贝与深拷贝
数组实际上是对象，所以 用 = 赋值，实际上是给的引用（浅拷贝）

如果确定数组的元素为原始类型数据（字符串，数组，布尔，null,undefined）,可以使用slice()或concat()方法实现近似的值copy效果：



```
let c1 = array1.slice(); //array1与c1值相同，但不存在引用关系，改变一个的值另一个不受影响
```

但实际上slice()，concat()等方法只能实现数组的**浅拷贝（即数组的每一项只能是原始类型的数据，如果数组的项包含引用类型，如数组（即js中的二维数组），对象等，以上方法复制的项只是引用）**

实现深拷贝的一种简单方法是JSON转化：

```
let jsonc = JSON.parse(JSON.stringify(array1));
```

这种方法可以变相的实现深拷贝,但也有其限制：

首先，数组中的项如果是undefined，那么转换后将变为null
如果数组的项为对象，那么对象之间不可相互引用。会造成循环引用，无法JSON序列化。


参考：

js 数组拷贝
https://juejin.im/entry/58217da92f301e005c2de257

javaScript中浅拷贝和深拷贝的实现
https://github.com/wengjq/Blog/issues/3




