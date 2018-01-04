## this 的指向
**类的方法内部如果含有this，它默认指向类的实例**。但须非常小心，一旦单独使用该方法，很可能报错。



```
class Logger {
  printName(name = 'there') {
    this.print(`Hello ${name}`);
  }

  print(text) {
    console.log(text);
  }
}

const logger = new Logger();
const { printName } = logger;
printName(); // TypeError: Cannot read property 'print' of undefined
```



上面代码，printName方法中的this，默认指向Logger类的实例。但如果**将这个方法提取出来单独使用，this会指向该方法运行时所在的环境**，因找不到print方法而报错。

解决方法一（最简单）：在类的构造方法中绑定this



```
class Logger {
  constructor() {
    this.printName = this.printName.bind(this);
  }

  // ...
}
```



方法二：使用箭头函数（自动绑定this）



```
class Logger {
  constructor() {
    this.printName = (name = 'there') => {
      this.print(`Hello ${name}`);
    };
  }

  // ...
}
```



方法三：使用Proxy，获取方法时，自动绑定this。



```
function selfish (target) {
  const cache = new WeakMap();
  const handler = {
    get (target, key) {
      const value = Reflect.get(target, key);
      if (typeof value !== 'function') {
        return value;
      }
      if (!cache.has(value)) {
        cache.set(value, value.bind(target));
      }
      return cache.get(value);
    }
  };
  const proxy = new Proxy(target, handler);
  return proxy;
}

const logger = selfish(new Logger());
```

