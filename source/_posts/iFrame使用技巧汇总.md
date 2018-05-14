---
title: iFrame使用技巧汇总
toc: true
comments: true
date: 2018-05-13 22:01:51
tags:
- IFRAME
- iOS iframe width
categories:
- HTML5
---

该博文主要是记录在开发过程中使用`iframe`时遇到问题，收集的解决方法汇总。

### `iframe`移动设备垂直滚动问题
移动开发过程中使用`iFrame`时，出现在`iOS10`以上系统出现滚动异常问题，该问题已经有国外大拿提供了解决方案，请看我的另一篇博文[《解决iframe嵌入页面在iOS不能滚动问题》](https://youcanping.cn/2017/12/28/iframe-scroll-in-ios/)

### 禁止`iframe`产生历史记录
#### 方式一
`url`链接变化，不通过改变`iframe`的`src`属性，而是每次都创建一个新的`iframe`指向新的`url`;
```js
   var ifr =  document.createElement('iframe');
    ifr.src = 'https://www.jd.com';
    document.body.appendChild(ifr);
```
#### 方式二
通过操作`iFrame`的`location`来改变`iFrame`指向的`url`;
```js
    var ifr = document.getElementById('ifr');
    ifr.contentWindow.location.replace('https://www.jd.com');
```

### `iframe`页面使用`viewport`进行页面缩放问题
在移动开发过程中，嵌入的三方页面，使用[高清屏页面渲染方案](http://www.aliued.com/?p=3166)，这时就会出现子页面会超出页面容器放大了，出现该问题，是因为父子容器设置的缩放比不一致导致的。
#### 解决方法
* 父子容器设置的`viewport`保持一致即可。
* 父容器不设置`viewport`，就不出现父子容器`viewport`冲突问题。

#### 示例
* 父容器`viewport`设置

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0,minimum-scale=1.0,user-scalable=0" />
```
* `iframe`子页面使用高清屏解决方案，进行页面缩放，如`iPhone5`;

```html
<meta name="viewport" content="width=640,initial-scale=0.5,maximum-scale=0.5, minimum-scale=0.5,user-scalable=no">
```

### `iframe`在`iOS`部分机型宽度问题
#### 问题描述
`iframe`嵌入的页面有横向滚动模块，使用了`overflow-x: auto;`样式，这个时候嵌入页面的宽度会撑大页面，导致`iframe`出现了横向滚动。      
<img src="http://our9i4zgx.bkt.clouddn.com/QQ20180514-222410.gif" style="width:320px;">

#### 解决方式
```html
<div style="overflow: auto;-webkit-overflow-scrolling:touch;width:100%;height:100%;">
    <iframe src="http://h5.m.taopiaopiao.com" frameborder="0" height="100%" scrolling='no' style="width: 1px; min-width: 100%; *width: 100%;"></iframe>
  </div>
```
### 移动端`iframe`终极方案
```css
         .iframe-container{
             position: fixed;
             top: 0;
             left: 0;
             z-index: auto;
             overflow: auto;
             -webkit-overflow-scrolling:touch;
             width:100%;
             height:100%;
         }
         .iframe-container iframe{
             width: 1px;
             *width: 100%;
             min-width: 100%;
             /*width: 100%;*/
             /*height: 100%;*/
         }
```
```html
    <!--height="100%"要写在行内，写在class中不生效-->
    <iframe src="https://h5.m.taopiaopiao.com" scrolling='no' frameborder="0" height="100%"></iframe>
```
![](http://our9i4zgx.bkt.clouddn.com/QQ20180514-223503@2x.png)




 
       
      





