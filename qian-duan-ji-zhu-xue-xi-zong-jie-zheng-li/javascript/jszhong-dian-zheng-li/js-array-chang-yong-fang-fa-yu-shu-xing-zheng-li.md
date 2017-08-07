# js Array
## js Array 常用方法与属性整理

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
返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。
说明

**注意：该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。**

http://www.w3school.com.cn/jsref/jsref_slice_array.asp

### sort() 排序

```
arrayObject.sort(sortby)

```

sortby	可选。规定排序顺序。**必须是函数**。

http://www.w3school.com.cn/jsref/jsref_sort.asp

### unshift() 向数组**开头添加一个或更多元素**，并返回新的长度。

```
arrayObject.unshift(newelement1,newelement2,....,newelementX)
```

http://www.w3school.com.cn/jsref/jsref_unshift.asp

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







