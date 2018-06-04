## rem 与 flex
### lib-flexible 可伸缩布局方案
https://github.com/amfe/lib-flexible

使用Flexible实现手淘H5页面的终端适配
https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html

## vw实现移动端适配（推荐）
利用视口单位实现适配布局
https://aotu.io/notes/2017/04/28/2017-4-28-CSS-viewport-units/index.html

再聊移动端页面的适配
https://www.w3cplus.com/css/vw-for-layout.html

如何在Vue项目中使用vw实现移动端适配**（推荐，最新的最完善的vw方案）**
https://www.w3cplus.com/mobile/vw-layout-in-vue.html


### 实践步骤：
安装：

npm i postcss-aspect-ratio-mini postcss-px-to-viewport postcss-write-svg postcss-cssnext p

.postcssrc.js文件对新安装的PostCSS插件进行配置：


```
module.exports = {
    "plugins": {
        "postcss-import": {},
        "postcss-url": {},
        "postcss-aspect-ratio-mini": {}, 
        "postcss-write-svg": {
            utf8: false
        },
        "postcss-cssnext": {},
        "postcss-px-to-viewport": {
            viewportWidth: 750,     // (Number) The width of the viewport.
            viewportHeight: 1334,    // (Number) The height of the viewport.
            unitPrecision: 3,       // (Number) The decimal numbers to allow the REM units to grow to.
            viewportUnit: 'vw',     // (String) Expected units.
            selectorBlackList: ['.ignore', '.hairlines'],  // (Array) The selectors to ignore and leave as px.
            minPixelValue: 1,       // (Number) Set the minimum pixel value to replace.
            mediaQuery: false       // (Boolean) Allow px to be converted in media queries.
        }, 
        "postcss-viewport-units":{},
        "cssnano": {
            preset: "advanced",
            autoprefixer: false,
            "postcss-zindex": false
        }
    }
}

```



**用到的一些技术简介：**
postcss-cssnext其实就是cssnext。该插件可以让我们使用CSS未来的特性，其会对这些特性做相关的兼容性处理。

cssnano主要用来压缩和清理CSS代码。

postcss-px-to-viewport插件主要用来把px单位转换为vw、vh、vmin或者vmax这样的视窗单位，也是vw适配方案的核心插件之一。






