---
title: CSS-清除浮动(.clearfix)
toc: true
comments: true
date: 2018-07-08 23:40:03
tags:
- clearfix
- 清除浮动
categories:
- CSS
---

## 浮动带来的问题
我们在网页中经常会使用`float`来进行图文混排, 但当文字在父容器中的高度比浮动元素小时，就会出现浮动元素溢出父容器，如果我们给父容器设置边框，就会出现如下效果：
* ![](http://our9i4zgx.bkt.clouddn.com/Jietu20180708-234417@2x.png)    
如果容器内的元素都是浮动元素，则父容器的高度将是0，我们称之为高度坍塌，效果如下：
* ![](http://our9i4zgx.bkt.clouddn.com/Jietu20180708-235219@2x.png)
## 清除浮动的方法
为了解决上述浮动带来的问题，达到如下效果，有人总结了以下方法：
* ![](http://our9i4zgx.bkt.clouddn.com/Jietu20180709-000059@2x.png)

### 方案一
设置父容器的高度。
* 优点：简单、粗暴。
* 缺点：需要知道子元素的高度和个数来确定父容器的高度，不够灵活。

### 方案二
在浮动元素的末尾添加空标签，设置`clear:both`。
* 优点：简单、粗暴。
* 缺点：需要添加无用的标签，不利于样式与结构分离，不易于后期维护。

### 方案三
给父容器也设置浮动`float`。
* 优点：简单、粗暴
* 缺点：改变父容器的布局，会影响父容器的后面元素的位置。

### 方案四
给父容器设置`overflow:hide/auto`。
* 优点：简单、代码量少。
* 缺点：会影响子元素内容溢出的显示问题。

### 方案五
给父容器设置`display:table`。
* 优点：简单、代码量少。
* 缺点：改变了父容器盒子模型属性，会造成一些未知影响。

### 方案六
```css
.clearfix:after{
    content: '';    //有人也会设置 \200B 零宽度空格
    display: block;
    clear: both;
}
.clearfix{
    *zoom: 1;       //对 IE/6/7 的兼容性处理原理未知
}
```
* 优点：不改变父容器的布局和盒子模型，没有副作用。
* 缺点：代码量多。

### 方案七
```css
.clearfix:before,.clearfix:after{
    content: '';
    display: table;
}
.clearfix:after{
    clear: both;
}
.clearfix{
    *zoom: 1;       //对 IE/6/7 的兼容性处理原理未知
}
```
* 原理：`display: table`会生成匿名元素`table-cell`触发`BFC`。
* 优点：不改变父容器的布局和盒子模型，没有副作用。
* 缺点：代码量多。
## 总结
`方案六`合`方案七`为终极解决方案，选一个即可。




