---
title: 移动端问题汇总
toc: true
comments: true
date: 2018-06-28 14:52:30
tags:
- 移动端问题汇总
categories:
- 问题汇总
---

## 移动端:active伪类无效的解决方法
### 解决方法
* Safari Mobile 默认不使用:active 状态，除非元素上或<body>上有一个touchstart 事件处理器。
```html
<body ontouchstart=""> <!-- Hack to activate :active CSS selector on iOS browsers.-->
```
* 给`body`添加`touchstart`事件。
```js
document.body.addEventListener('touchstart', function () { //...空函数即可});
```
### 参考资料
> * [移动端:active伪类无效的解决方法](https://blog.csdn.net/freshlover/article/details/43735273)
> * [MDN-web-docs :active](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:active)

## 监听文档是否处于激活状态
### 解决方法
使用H5新的监听文档可见状态事件`visibilityChange`判断当前页面是否处于激活状态
* 方式一
```js
var hiddenProperty = 'hidden' in document ? 'hidden' :
    'webkitHidden' in document ? 'webkitHidden' :
        'mozHidden' in document ? 'mozHidden' :
            null;
var visibilityChangeEvent = hiddenProperty.replace(/hidden/i, 'visibilitychange');
var onVisibilityChange = function(){
    if (document[hiddenProperty]) {
        console.log('页面非激活');
    }else{
        console.log('页面激活');
    }
}
document.addEventListener(visibilityChangeEvent, onVisibilityChange);
```
* 方式二
```js
// 设置隐藏属性和改变可见属性的事件的名称
var hidden, visibilityChange;
if (typeof document.hidden !== "undefined") { // Opera 12.10 and Firefox 18 and later support
  hidden = "hidden";
  visibilityChange = "visibilitychange";
} else if (typeof document.msHidden !== "undefined") {
  hidden = "msHidden";
  visibilityChange = "msvisibilitychange";
} else if (typeof document.webkitHidden !== "undefined") {
  hidden = "webkitHidden";
  visibilityChange = "webkitvisibilitychange";
}
function handleVisibilityChange() {
  if (document[hidden]) {
    // 非激活状态
  } else {
    //页面激活
  }
}
document.addEventListener(visibilityChange, handleVisibilityChange, false);
```
### 参考资料
> * [MDN-web-docs Page_Visibility_API](https://developer.mozilla.org/zh-CN/docs/Web/API/Page_Visibility_API)


