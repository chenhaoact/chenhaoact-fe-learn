## Web 应用清单文件 (manifest.json)

在文本文件中提供了应用相关信息 (如应用名称、作者、图标和描述)。

Web 应用清单可使用户将 Web 应用安装到设备的主屏幕上，并允许开发者自定义启动画面、模板颜色，甚至是打开的 URL 。

### 例子

```
{
  "name": "Progressive Times web app", // name 用作当用户被提示安装应用时出现的文本
  "short_name": "Progressive Times", // 应用安装后出现在用户主屏幕上的文本
  "start_url": "/index.html", // 用户从设备的主屏幕开启 Web 应用时所出现的第一个页面
  "display": "standalone", // 开发者希望他们的 Web 应用如何向用户展示，后面详细说明
  "oriention": "landscape", // 方向，portrait 竖屏， landscape 横屏
  "theme_color": "#FFDF00", // 对浏览器的地址栏进行着色，以符合网站的主色调
  "background_color": "#FFDF00",
  // Web 应用被添加到设备主屏幕时所显示的图标
  "icons": [{  
      "src": "homescreen.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "homescreen-144.png",
      "sizes": "144x144",
      "type": "image/png"
    }
  ]
}
```

关于显示模式display的选项：

fullscreen - 打开 Web 应用并占用整个可用的显示区域（全屏效果，连手机系统顶栏显示也没了）。
**standalone** - 打开 Web 应用以看起来像一个独立的原生应用。此模式下，用户代理将**排除诸如 URL 栏等标准浏览器 UI 元素**，但可以包括诸如状态栏和系统返回按钮的其他系统 UI 元素。
minimal-ui - 此模式类似于 fullscreen，但为终端用户提供了可访问的最小 UI 元素集合，例如，后退按钮、前进按钮、重载按钮以及查看网页地址的一些方式。
browser - 使用操作系统内置的标准浏览器来打开 Web 应用（相当于唤起浏览器打开页面，浏览器里可以切换不同的之前已打开的tab（即使与本页面无关））。display 属性是可选项，默认以 browser 模式来显示。


所有具体的配置项参考：
Web App Manifest - MDN
https://developer.mozilla.org/en-US/docs/Web/Manifest


## 引用

在网页的 head 标签中使用 link 标签来引用 Web 应用的清单文件。

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Progressive Times</title>
    <link rel="manifest" href="/manifest.json">  
  </head>
  <body>
    ...
  </body>
</html>
```

webpack的项目推荐使用webpack-pwa-manifest插件来用配置自动生成manifest。json及图标等文件
https://github.com/arthurbergmz/webpack-pwa-manifest

## 参考

Web App Manifest - MDN
https://developer.mozilla.org/en-US/docs/Web/Manifest

web-app-manifest 谷歌开发者文档
https://developers.google.com/web/fundamentals/web-app-manifest/


