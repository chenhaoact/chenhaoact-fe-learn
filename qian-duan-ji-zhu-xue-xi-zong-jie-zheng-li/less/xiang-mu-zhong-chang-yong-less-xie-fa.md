
##（1）通过样式类名自由控制字体大小



```less
.text-size-make(88);
.text-size-make(@size) when (@size > 0) {
  .text-size-make((@size - 2));
  .text-size-@{size},
  .font-size-@{size}{
    font-size: @size * 1px !important;
  }
}

```

这样就可以使用 如 text-size-16  font-size-18 这样的样式类直接控制字体大小，不需要常用的字体大小一个一个去写。
