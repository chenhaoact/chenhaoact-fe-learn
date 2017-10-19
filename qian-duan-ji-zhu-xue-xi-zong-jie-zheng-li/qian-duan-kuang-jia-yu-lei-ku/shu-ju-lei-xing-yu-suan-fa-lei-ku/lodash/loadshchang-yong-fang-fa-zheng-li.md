#loadsh常用方法整理

##_.isEmpty(value)

判断值，数组，对象是否为空

##_.assign()  别名：_.extend
合并对象

## _.keys(obj)
返回对象的属性名（以字符串形式放在数组里）


```
const obj = {
   a: 1,
   b: 2
}

_.keys(obj); // ['a', 'b'] 

```

参考：
http://lodashjs.com/docs/#_keysobject
## 