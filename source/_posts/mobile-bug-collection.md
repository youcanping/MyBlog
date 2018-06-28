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
> * [MDN-:active](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:active)