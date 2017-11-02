## 一 数组（Array）
### 1 _.chunk()  等份拆分数组


```
_.chunk(array, [size=1])

```

将 array 拆分成多个 size 长度的块，把这些块组成一个新数组。 如果 array 无法被分割成全部等长的块，那么最后剩余的元素将组成一个块。

例子：

```
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
```
### 2._.concat() 拼接成新数组（将数组或值）


```
_.concat(array, [values])
```



例子：


```
var array = [1];
var other = _.concat(array, 2, [3], [[4]]);
// => [1, 2, 3, [4]]
 
```



### 3. _.difference() 返回前一个数组不在后一个数组中的的值组成的数组

```
_.difference(array, [values])
```



例子：

```
_.difference([1, 2, 3], [4, 2]);
// => [1, 3]
```


### 4._.drop() 将array前 n 个元素去除，返回剩余部分


```
_.drop(array, [n=1])
```

参数
[n=1] (number): 去掉的元素个数。

例子：

```
_.drop([1, 2, 3], 2);
// => [3]
```



### 5. _.fill() 使用 value 值来填充（也能替换） array 


```
_.fill(array, value, [start=0], [end=array.length])
```

从start位置开始, 到end位置结束（但不包含end位置）

例子：



```
_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8], '*', 1, 2);
// => [4, '*', 8]
```


### 6._.findIndex() 返回符合条件的第一个元素的索引


```
_.findIndex(array, [predicate=_.identity], [thisArg])
```

该方法类似 _.find，区别是该方法返回的是符合 predicate条件的第一个元素的索引，而不是返回元素本身. 

例子：



```
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false }
];

_.findIndex(users, function(chr) {
  return chr.user == 'barney';
});
// => 0
```

同类方法：
_.findLastIndex()
类似 _.findIndex ，区别是其从右到左遍历数组. 

### 7. _.flatten() 嵌套数组的维数减少


```
_.flatten(array, [isDeep])
```

flattened（平坦）. 如果 isDeep 值为 true 时，嵌套数组将递归为一维数组, 否则只减少嵌套数组一个级别的维数.

例子：

```
_.flatten([1, [2, 3, [4]]]);
// => [1, 2, 3, [4]]

// using `isDeep`
_.flatten([1, [2, 3, [4]]], true);
// => [1, 2, 3, 4]
```


### 2.


```

```



例子：



```

```


### 2.


```

```



例子：



```

```

















