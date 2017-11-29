## 对象

### _.keys() 返回对象的key组成的数组（顺序不能保证）

注意：
如果是数组或字符串类型返回的是下标组成的数组。

语法

```
_.keys(object)
```

例子


```
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)
 
_.keys('hi');
// => ['0', '1']   数组或字符串类型返回的是下标组成的数组
```



