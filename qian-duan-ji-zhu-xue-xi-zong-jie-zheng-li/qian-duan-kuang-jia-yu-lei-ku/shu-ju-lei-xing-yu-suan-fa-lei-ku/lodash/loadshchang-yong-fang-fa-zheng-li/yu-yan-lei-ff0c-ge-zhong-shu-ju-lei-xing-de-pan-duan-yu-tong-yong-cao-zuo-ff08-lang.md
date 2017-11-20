### _.clone() 浅拷贝（建议：不能确定数组里数据类型的时候直接就使用cloneDeep更保险）
子元素是基本数据类型时（字符串，数字，布尔，null,undefined）可以拷贝其值，否则拷贝的是引用。 

### _.cloneDeep() 深拷贝
**即使对象或数组内部的元素是数组或对象等复杂的数据类型，也能够拷贝其值，而非拷贝引用。**

### _.isArray() 判断是否为数组

语法

```
_.isArray(value)
```

例子

```
_.isArray([1, 2, 3]);
// => true
 
_.isArray(document.body.children);
// => false
 
_.isArray('abc');
// => false
```

### _.isEmpty() 判断是否为空
语法

```
_.isEmpty(value)
```

检查值是否为空对象，集合，映射或集合。

如果对象没有自己的可枚举字符串键控属性，则它们被认为是空的。

如果参数对象，数组，buffers，字符串或类似jQuery的集合的length为0，则它们被认为是空的。类似地，如果map和set的size为0，则认为它们是空的。

**（注意：单个数字或字符是判断为空的）**

```
_.isEmpty(null);
// => true
 
_.isEmpty(true);
// => true
 
_.isEmpty(1);  //注意这里单个数字或字符也是空的
// => true
 
_.isEmpty([1, 2, 3]);
// => false
 
_.isEmpty({ 'a': 1 });
// => false
```

### _.isEqual() 判断值是否相同

TODO?





