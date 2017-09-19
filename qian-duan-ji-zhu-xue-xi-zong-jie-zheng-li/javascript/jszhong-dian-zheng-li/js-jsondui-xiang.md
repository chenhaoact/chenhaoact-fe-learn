# js JSON对象

## 对象与 JSON 字符串的转化

### 1. JSON.stringify() 对象转换成json字符串

给后端传参数时，对象和数组类数据一般转为json字符串：


```
const list = [a:'a'];

ajax(
  { 
    api:'...',
    data:{
      list: JSON.Stringify(list)
    }
  }
)

```



### 2. JSON.parse() json字符串解析成对象。

参考：
https://www.zhihu.com/question/19884767