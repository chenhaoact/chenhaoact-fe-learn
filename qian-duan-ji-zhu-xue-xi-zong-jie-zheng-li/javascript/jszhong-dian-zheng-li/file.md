# File
## 一 简介
**文件(File) 接口提供有关文件的信息，并允许网页中的 Js 脚本访问其内容。**

通常情况下， File 对象是来自用户在一个   `<input>` 元素上选择文件后返回的 FileList 对象,也可以是来自由拖放操作生成的 DataTransfer 对象，或者来自 HTMLCanvasElement 上的 mozGetAsFile() API。

**File 对象是特殊类型的 Blob，且可以用在任意的 Blob 类型的 context 中**。比如说， FileReader, URL.createObjectURL(), createImageBitmap(), **及 XMLHttpRequest.send() 都能处理 Blob  和 File**。


## 二 使用
TODO

## 参考
### 待学习
[《JavaScript 标准参考教程（alpha）》，阮一峰Web API - 文件和二进制数据的操作](http://javascript.ruanyifeng.com/htmlapi/file.html)

[MDN Web API - File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)