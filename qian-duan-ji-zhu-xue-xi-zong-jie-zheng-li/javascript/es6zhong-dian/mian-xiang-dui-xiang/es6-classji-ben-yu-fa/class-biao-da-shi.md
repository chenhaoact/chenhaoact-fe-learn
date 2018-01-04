## Class 表达式
与函数一样，类也可以使用表达式的形式定义。



```
const MyClass = class Me {
  getClassName() {
    return Me.name;
  }
};
```

上面代码用表达式定义类。注意，**这个类的名字是MyClass而不是Me**，**Me只在 Class 内部代码可用**，指代当前类。

如果类的内部没用到的话，可以省略Me，写成下面的形式。

```
const MyClass = class { /* ... */ };
```

采用 Class 表达式，可写出立即执行的 Class实例。 


