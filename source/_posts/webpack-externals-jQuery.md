---
title: webpack使用jQuery的解决方式
toc: true
comments: true
date: 2018-01-15 14:32:34
tags: 
 - WEBPACK 
 - JQUERY
categories: 
 - WEBPACK
---
## webpack引入jquery报错
jQuery作为老牌的web前端利器已经好多年，虽然有很多人说jQuery性能低等，出现了很多替代品，但不可否认，对开发轻量级别的应用来说还是很好用，jQuery插件丰富，还是很令人割舍不下的。    
最近项目引入了webpack打包工具，由于用到了jQuery和jQuery的一些插件，如果jquery.js用webpack构建，插件会因为找不到而报错。 

```bash
ERROR in ./src/pages/common/support/js/jquery.mobile-1.4.5.js
Module not found: Error: Can't resolve 'jquery' in 'C:\Users\Administrator\Desktop\web_online\src\pages\common\support\js'
 @ ./src/pages/common/support/js/jquery.mobile-1.4.5.js 18:2-21:4

ERROR in ./src/pages/common/support/js/jquery.touchSwipe.js
Module not found: Error: Can't resolve 'jquery' in 'C:\Users\Administrator\Desktop\web_online\src\pages\common\support\js'
 @ ./src/pages/common/support/js/jquery.touchSwipe.js 154:4-31 157:12-29
```

## 我的解决方式
1. HTML页面直接引入jQuery,考虑jQuery这种库不会经常改的，页面缓存也无所谓，缓存更好，用到的三方库也用HTML引入的方式。

```html
<script src="../common/support/js/jquery-1.8.2.min.js"></script>
<script src="../common/support/js/jquery.mobile-1.4.5.js"></script>
```

2. 使用CopyWebpackPlugin插件,把第三方支持库直接拷贝到`dist/`目录下，绕过webpack打包构建，直接复制的目标文件夹下，注意jQuery在`src/`和`dist/`下的目录结构保持一致。
3. 在webpack.config.js中进行配置externals，告诉webpack下jquery不需要打包了，不然会报错。

```javascript
externals:{
   jquery:"window.$",
   $:"window.$"
},
plugins:[
    //...
]
```




