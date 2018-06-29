# next()、throw()、return() 的共同点

三个方法本质上是同一件事，它们的作用都是让 Generator 函数恢复执行，并且使用不同的语句替换yield表达式。

next()是将yield表达式替换成一个值。

throw()是将yield表达式替换成一个throw语句。

return()是将yield表达式替换成一个return语句。