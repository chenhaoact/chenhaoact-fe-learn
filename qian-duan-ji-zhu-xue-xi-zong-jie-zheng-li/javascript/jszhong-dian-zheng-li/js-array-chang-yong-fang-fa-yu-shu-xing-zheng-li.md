# js Array
## js Array 属性与常用方法整理

## 1. 属性

### length

null或undefined也会计入length中：


```
[undefined, 1].length  // 2
[null, 1].length  //2
```



**因此读length(包括使用slice等字符串或数组的方法)之前务必保证元素不为null或undefined,否则js会抛异常从而可能让整个页面都渲染不出来！！！**

如超过长度截取前n个并显示...：

```
{
  a != null && a.length >=16 ? 
  a.slice(0,16) + '...'
  :
  a
}
```

**这样利用且（&&）表达式的特性，前面为false时，就不会去执行后面的，也就不会报错了。（注意这里的顺序，slice是写在 != null 肯定为ture的语句下的，不能放后边！,所以这里用的>=）**

**读数组或字符串的length属性包括使用slice等字符串或数组的方法时必须这样处理，否则会引发故障！！！**


## 2. 方法
### indexOf() 返回某值在数组（字符串也可以用）中首次出现的位置（检索值没出现则返回 -1）
语法

```
.indexOf(searchvalue [,fromindex])
```

searchvalue	必需。规定需检索的字符串值。
fromindex	可选的整数参数。规定在字符串中开始检索的位置。


### push() 向数组的末尾添加一个或多个元素，并返回新的长度。

```
arrayObject.push(newelement1,newelement2,....,newelementX)
```

参数	描述
newelement1	必需。要添加到数组的第一个元素。
newelement2	可选。要添加到数组的第二个元素。
newelementX	可选。可添加多个元素。

返回值
把指定的值添加到数组后的新长度。

注意：
push() 方法可把它的参数顺序添加到 arrayObject 的尾部。它**直接修改 arrayObject，而不是创建一个新的数组**。push() 方法和 pop() 方法使用数组提供的先进后出栈的功能。

http://www.w3school.com.cn/jsref/jsref_push.asp


**数组里增加对象要注意**：

**对象的值相当于其引用，不能直接赋值，那样会指向同一个对象**，对一个操作也会影响另一个，需要去仅仅把值拷贝一份给新的对象，再添加到数组中：

```
//错误
addedTags.push（originTags[idx]）;

//正确
let tagToAdd = Object.assign({},originTags[idx])
tagToAdd.attr1 = true;
addedTags.push(tagToAdd);
```

### pop 删除并返回数组的最后一个元素
语法


```
arrayObject.pop()

```

例子


```
let a = [George,John,Thomas]
a.pop() //返回"Thomas",数组a变为[George,John]
```



### splice() 向/从数组中添加/删除项目，然后返回被删除的项目。
**注：该方法会改变原始数组**
```
arrayObject.splice(index,howmany,item1,.....,itemX)
```

参数	描述
index	必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
howmany	必需。要删除的项目数量。如果设置为 0，则不会删除项目。
item1, ..., itemX	可选。向数组添加的新项目。

返回值：
类型	描述
Array	包含被删除项目的新数组，如果有的话。

http://www.w3school.com.cn/jsref/jsref_splice.asp

### slice() 从已有的数组中返回选定的元素

```
arrayObject.slice(start,end)
```

参数	描述
start	必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。
end	可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。

返回值
返回一个新的数组，包含从 start 到 end （**截取包括start但不包括索引为end的元素**）的 arrayObject 中的元素。
说明

**注意：该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。**

例子


```
const a = [George,John,Thomas,James,Adrew,Martin]
b = a.slice(2,4) //b [Thomas,James]    a不变
```



http://www.w3school.com.cn/jsref/jsref_slice_array.asp

### sort() 排序

```
arrayObject.sort(sortby)

```

sortby	可选。规定排序顺序。**必须是函数**。

http://www.w3school.com.cn/jsref/jsref_sort.asp

### unshift() 向原数组**开头添加一个或更多元素**

并返回新的长度。

```
arrayObject.unshift(newelement1,newelement2,....,newelementX)
```

例子


```
var tmp = ['a','b'];
var len = tmp.unshift('c');
alert(tmp); // ['c','a','b']
```



http://www.w3school.com.cn/jsref/jsref_unshift.asp

类比方法：
**shift: 把数组的第一个元素从其中删除，并返回第一个元素的值。
**
### join()

把数组中的所有元素放入一个字符串。
元素是通过指定的分隔符进行分隔。



```
arrayObject.join(separator)
```

参数	描述
separator	可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。


### toString()
把数组转换为字符串，并返回结果。
数组中的元素之间用逗号分隔。
返回值与没有参数的 join() 方法返回的字符串相同。

```
arrayObject.toString()
```

实例：

```
var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"

document.write(arr.toString()) //输出：George,John,Thomas
```

### filter() 筛选，搜索

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

注意：
filter() 不会对空数组进行检测。
filter() 不会改变原始数组。

语法：


```
array.filter(function(currentValue,index,arr), thisValue)
```

参数：
1. function(currentValue, index,arr)	必须。函数，数组中的每个元素都会执行这个函数
函数参数:
（currentValue	必须。当前元素的值
index	可选。当期元素的索引值
arr	可选。当期元素属于的数组对象）

2. thisValue	可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。

实例：

```
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
}

ages.filter(checkAdult); //32,33,40
```

### includes() 判断一个数组是否包含一个指定的值

语法


```
arr.includes(searchElement)
arr.includes(searchElement, fromIndex)
```



例子


```
let a = [1, 2, 3];

a.includes(2); 
// true 

a.includes(4); 
// false
```

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes


## 二 js array重点归纳整理
### 1. 重点整理！调用后原数组被改变的方法
push

### 2. 重点整理！调用后（只是返回新的结果）原数组没有被改变的方法
concat

### 3. Js中 map、foreach、reduce的区别
forEach()和map()遍历共同点：

    1.都是循环遍历数组中的每一项。
    2.里面每一次执行匿名函数都支持3个参数：数组中的当前项item,当前项的索引index,原始数组input。
    3.只能遍历数组。

不同点：
**.forEach() 没有返回值。**


```
arr[].forEach(function(value,index,array){
　　//do something
}) 
```

.map() 有返回值，可以return 出来。



```
arr[].map(function(value,index,array){

　　//do something

　　return XXX

})
```

**reduce()** 方法对累加器和数组中的**每个元素（从左到右）应用一个函数，将其减少为单个值。**


### 4. 注意：forEach和map循环都是会全部遍历一遍的，不能用break跳出循环，如果想在中途判断条件跳出循环，需要用 for循环

```
for (var i=0;i<cars.length;i++)
{
   if(i=3) {
     
     break; 
   }
}
```









