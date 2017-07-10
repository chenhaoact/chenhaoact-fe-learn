#less

css预处理技术已经发展的比较成熟了，通过css预处理技术可以很好的提升css的编程性，提高css代码的开发效率和可维护性，目前比较热门的相关技术有Sass、Less CSS、Stylus、Compass等，最近也陆续在项目中用到了这些技术，所以就来个总结吧，**本文为系列文章第二篇，主要讨论Less**。

相比Sass而言,Less要简单易上手一些，但是编程性较Sass而言，略有不足，所以也有人说它更适合设计师学习，但这并不妨碍它的广泛使用，因为Less本身的语法就已经很够用了，Twitter大名鼎鼎的Bootstrap项目就是基于Less构建而成，以下是前端项目中经常会用到的一些Less语法：

##一 注释
less注释一,会被编译到css
```less
/**/　　　　
```
less注释二,不会被编译到css,建议之后只维护less,所以可多用这种注释
```less
//　　
```

##二 变量
定义变量用 @变量名:变量值;  使用该变量值时用 @变量名

```less
@width: 300px;
body {
  background-color: white;
}

.div1 {
  width: @width;
}
```

##三 混合（mixin）
混合可以将一个定义好的class A轻松的引入到另一个class B中，从而简单**实现class B继承class A中的所有属性。还可以带参数地调用。**

比如定义一个样式类.border,直接用到另一个样式类.box里,另一个样式类就很方便的具有了这个类的样式,很好的实现了css代码的复用;
再比如有一个.box2,它和.box有一些属性相同,那就直接继承.box再做特定的修改即可：

```less
.border {
  border: solid 1px black;
}

.box {
  .border; //注意这里！
}

.box2 {
  .box; //还有这里！
  margin: 20px;
}　　
```


**混合（mixin）:可带参数**,以实现**传入变量**参数来用同一个样式类生成各种不同的样式：

```less
.border2(@border_width) { //定义变量参数
  border: @border_width solid black;
}

.box3 {
  .border2(5px); //参数位置传入变量以控制不同的样式
}

.box4 {
  .border2(10px);
}
```

**混合（mixin）参数可带默认值(多个参数之间使用逗号隔开)**

```less
.border3(@border_width2:5px) {
  border: @border_width2 solid black;
}

.box5 {
  .border3(); //
}
```

一些常见的兼容性写法就可以用混合封装起来进行简化:
```less
.border_radius(@border_radius:2px) {
  border-radius: @border_radius;
  -moz-border-radius: @border_radius;
  -webkit-border-radius: @border_radius;
}
```

##四 模式匹配

有些情况想根据传入的参数来改变混合的默认呈现,比如：

下面**通过less模式匹配,定义不同样式模式**的三角(top模式和bottom模式),但**无论哪种模式,@_(放在模式参数位置)定义的样式所有模式都公有**。

```less
.triangle(@_,@w,@c) { //@_模式定义的样式是所有模式都公有的部分
  width: 0;
  height: 0;
  overflow: hidden;
}

.triangle(top,@w,@c) { //朝上的三角,这里用到了CSS的boder画三角
  border-width: @w;
  border-color: transparent transparent @c transparent; 
  border-style: dashed dashed solid dashed;
}

.triangle(bottom,@w,@c) { //朝下的三角
  border-width: @w;
  border-color: @c transparent transparent transparent;
  border-style: solid dashed dashed dashed;
}

.triangle2 {
  .triangle(bottom, 20px, red);
}

.triangle3 {
  .triangle(top, 30px, green)
}
```

##五 运算(对变量进行加减乘除等)

```less
@box_width: 100px;
.box6 {
  width: (@box_width - 10)*2;
}
```

##六 嵌套

可以在**一个选择器中直接嵌套另一个选择器来实现继承，这样很大程度减少了代码量，并且代码看起来结构更加清晰：**

```less
.list1 {
  width: 600px;
  height: 600px;

  li { //相当于在外边写 .list li{}
    height: 20px;

    a {
      float: left;

      //&代表上一层选择器,所以这样写相当于 .list a:hover{}
      &:hover {
        color: red;
      }
    }
  }
}
```

##七 @arguments
@arguments包含了所有传递进来的参数. 如果你不想单独处理每一个参数的话就可以像这样写:

```less
.box-shadow (@x: 0, @y: 0, @blur: 1px, @color: #000) {
  box-shadow: @arguments; //相当于()参数里的值放到了这
  -moz-box-shadow: @arguments;
  -webkit-box-shadow: @arguments;
}

.box-shadow(2px, 5px);
```

##八 避免编译

有时候需要输出一些不正确的CSS语法或者使用一些 LESS不认识的专有语法.
//要输出这样的值我们可以在字符串前加上一个 ~, 例如:
```less
.class1 {
  filter: ~"ms:alwaysHasItsOwnSyntax.For.Stuff()";  //css中会是 filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
}
```

##九 Less参考资料

1 完整的Less中文文档：
http://www.bootcss.com/p/lesscss/