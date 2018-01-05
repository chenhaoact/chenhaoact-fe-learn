## 类的继承相关方法
### 1. Object.getPrototypeOf() 从子类上获取父类



```
Object.getPrototypeOf(ColorPoint) === Point
// true
```


因此，**可用这个方法判断，一个类是否继承了另一个类**。