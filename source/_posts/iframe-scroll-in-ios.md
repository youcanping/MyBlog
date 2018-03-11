---
title: 解决iframe嵌入页面在iOS不能滚动问题
toc: true
comments: true
date: 2017-12-28 15:06:05
tags: 
- HTML
- IFRAME
categories:
- HTML5
---
## 问题描述
最近在写移动端模块页面，需要嵌入三方的页面，该页面有上拉加载更多的功能，但是使用iframe嵌入到我的web app中出现了不能滚动的问题。    
网上查询解决方式一直找不到很好的方式，无意中看到了一篇博客解决了我的燃眉之急，用很巧妙的方式化解了这个问题。    
原文链接 [scroll-iframes-ios](https://davidwalsh.name/scroll-iframes-ios)

## 解决方式
### 在iframe外面包裹一个div。
```html
<div class="scroll-wrapper">
	<iframe src=""></iframe>
</div>
```
### 给该div添加css触屏滚动属性。
```css
.scroll-wrapper {
	-webkit-overflow-scrolling: touch;
  	overflow-y: scroll;
    
	/* 在这里设置外层div的大小和定位样式 */
}

.scroll-wrapper iframe {
	/* 设置iframe的样式 */
}
```
### 我的页面需要全屏显示嵌入的页面，添加如下样式。
```css
.scroll-wrapper {
    position: fixed;
    right: 0;
    bottom: 0;
    left: 0;
    top: 0;
    -webkit-overflow-scrolling: touch;
    overflow-y: scroll;
}
.scroll-wrapper iframe {
    border: none;
    height: 100%;
    width: 100%;
}
```
