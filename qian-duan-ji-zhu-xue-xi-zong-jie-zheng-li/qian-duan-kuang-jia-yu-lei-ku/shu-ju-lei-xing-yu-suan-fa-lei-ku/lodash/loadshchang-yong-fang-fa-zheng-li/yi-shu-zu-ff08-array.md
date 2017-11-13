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

同类方法还有
_.differenceBy
_.differenceWith

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


### 8. _.fromPairs() 键值对数组转对象


```
_.fromPairs(pairs)
```

它是`_.toPairs`的反操作

例子：

```
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }
```


### 9. _.intersection() 取出各数组中全等的元素

使用 SameValueZero方式平等比较


```
_.intersection([arrays])
```



例子：



```
_.intersection([1, 2], [4, 2], [2, 1]);

// => [2]
```


同类方法还有
_.intersectionBy
_.intersectionWith


### 10. _.pull() 移除数组array中所有和 values 相等的元素 （常用！数组特定元素去除）

使用 SameValueZero 进行全等比较 

```
_.pull(array, [values])
```

Note: 不同于 _.without方法,此方法改变了数组 array（并不是原来的数组了）.

例子：

```
var array = [1, 2, 3, 1, 2, 3];

_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```

类似方法还有：
_.pullAll
_.pullAllBy
_.pullAllWith
_.pullAt


### 11. _.remove() 移除数组 array 中满足 predicate 条件的所有元素 

返回的是被移除元素数组. 

语法

```
_.remove(array, [predicate=_.identity], [thisArg])
```

Note: 
和方法 _.filter不一样, 此方法彻底改变数组array.


例子：



```
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4]
```


### 12. _.reverse()  逆序（第一个元素变最后一个，依次类推）

语法


```
_.reverse(array)
```



例子


```
var array = [1, 2, 3];
 
_.reverse(array);
// => [3, 2, 1]
```

### 13. _.union() 联合多个数组，创建一个没有重复元素的数组

语法


```
_.union([arrays])
```

例子


```
_.union([2], [1, 2]);
// => [2, 1]
```

### 14. _.unionBy() 联合多个数组，去除数组相互间重复的元素，重复的只留下一个（和_.union()相比它可通过某条件判断是否重复）

语法

```
_.unionBy([arrays], [iteratee=_.identity])
```

例子


```
_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]
 
// The `_.property` iteratee shorthand.
_.unionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```

### 15.  _.uniq()   一个数组内元素去重（而_.union()是联合多个数组为一个没有重复元素的数组）

语法


```
_.uniq(array)
```

例子

```
_.uniq([2, 1, 2]);
// => [2, 1]
```

相似的方法还有
_.uniqBy()
_.uniqWith()
可以支持按某些规则去重

### 16. _.without() 某数组中去掉某些元素从而形成一个新数组

语法

```
_.without(array, [values])
```

注意：
和_.pull不同，此方法是返回一个新数组

例子














