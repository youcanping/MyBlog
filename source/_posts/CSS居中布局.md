---
title: CSS居中布局
toc: true
comments: true
date: 2018-03-11 20:47:49
tags:
- CSS
categories:
- CSS
---
网上查阅了关于CSS居中布局的方案，决定自己亲自验证下，不能只是体验在理论层面上，做下总结。     
源码地址：[GITHUB](https://github.com/youcanping/github-demo/tree/master/align-layout)
### 水平居中布局
水平居中在线演示地址[DEMO](http://htmlpreview.github.io/?https://github.com/youcanping/github-demo/blob/master/align-layout/h-align-center/index.html)
#### 行内元素水平居中
使用`text-align: center;`进行行内元素、文字水平居中。
#### 块元素水平居中
使用`text-align: center;`和`margin:0 auto`;进行块元素水平居中。
低版本浏览器还需要设置`text-align: center`;
* 优点：兼容性好，可以兼容`IE6`和`IE7`。
* 缺点：子元素里的内容也会水平居中，需要在子元素中覆盖`text-align`属性。

```css
div.parent{
    text-align: center;
}
div.child{
    margin: 0 auto;
}
```
```html
<div class="parent">
    <div class="child">
        块元素 div
    </div>
</div>
```
#### 使用`display:table`实现水平居中布局
原理：给子元素设置属性`display:table;`和`margin:0 auto`实现子元素水平居中对齐。
优点：可以只设置子元素，实现水平居中对齐。
缺点：IE6,IE7不支持，IE8以上都支持
```css
.child{
display: table;
margin: 0 auto;
}
```
```html
<div>
    <div class="child">
    </div>
</div>
```
#### 使用absolute+transform
适用场景：移动端
原理：父容器设置相对定位，子容器设置绝对定位，子容器距离左边50%，然后用CSS3的transform的向左移动自身一半的距离。
优点：居中元素不会对其他元素产生影响
缺点：transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀
```html
<div class="parent">
     <div class="child">
         absolute+transform
     </div>
</div>
```
```css
.parent{
    position: relative;
}
.child{
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
}
```
#### 使用flex + justify-content
适用场景：移动端
原理：将父框设置为display:flex，再设置justify-content:center使子元素水平居中
优点：只设置父元素即可
缺点：低版本浏览器(ie6 ie7 ie8)不支持
```css
div.parent-flex {
    display: flex;
    justify-content: center;
}
```
```html
<div class="parent-flex">
    <p class="child">
        flex + justify-content
    </p>
</div>
```

### 水平垂直居中
#### 使用`display: table-cell;`和`vertical-align: middle;`进行垂直居中
原理：把父容器变成table,然后使用垂直居中属性把子元素居中。
优点：兼容性较好，IE8以上都支持。
缺点：嵌套太多，父容器不能单独设置宽高属性100%，需要制定具体的值，如果要实现百分比宽高，还需要把父容器放到`display:table;`的容器里才行。
```css
.table{
    display: table;
    width: 100%;
    height: 100%;
}
.parent{
    display: table-cell;
    /*垂直居中*/
    vertical-align: middle;
    /*水平居中*/
    text-align: center;
    width: 100%;
    height: 100%;
}
.child{
    width: 100px;
    display: inline-block;
}
```
```html
<div class="table">
    <div class="parent">
        <div class="child">
            &nbsp;
        </div>
    </div>
</div>
```
#### 使用绝对定位和设置外边距
原理：父容器设置为相对定位，子元素绝对定位`top:50%;left:50%;`，然后设置自身的外边距为自身宽度的一半
优点：兼容性好
缺点：需要提前知道子容器的宽高
```css
.parent{
    position: relative;
    width: 100%;
    height: 100%;
}
.child{
    position: absolute;
    width: 100px;
    height: 100px;
    top: 50%;
    left: 50%;
    margin-left: -50px;
    margin-top: -50px;
}
```
```html
<div class="parent">
    <div class="child">

    </div>
</div>
```
#### 绝对定位 + margin: auto
出自[小tip: margin:auto实现绝对定位元素的水平垂直居中](http://www.zhangxinxu.com/wordpress/2013/11/margin-auto-absolute-%E7%BB%9D%E5%AF%B9%E5%AE%9A%E4%BD%8D-%E6%B0%B4%E5%B9%B3%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD/)
原理：子容器绝对定位，上下左右都为0，外边距`margin:auto;`
优点：兼容性好，可以不用提前知道子容器的宽高
缺点：暂时没发现
```css
.parent{
    position: relative;
    width: 100%;
    height: 100%;
}
.child{
    position: absolute;
    width: 100px;
    height: 100px;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin:auto;
}
```
```html
<div class="parent">
    <div class="child">
    </div>
</div>
```
#### 使用absolute+transform实现水平垂直居中
适用场景：移动端
原理：使用CSS3`transform`移动自身的一半
优点：不用提前知道子容器的宽高，不影响其他元素的布局
缺点：兼容性不好
```css
.parent{
    position: relative;
    width: 100%;
    height: 100%;
}
.child{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    width: 60%;
    height: 60%;
}
```
```html
<div class="parent">
    <div class="child">

    </div>
</div>
```
#### 适用flex+align-items布局
优点：只设置父容器即可
缺点：兼容性不好
```css
.parent{
    display: flex;
    /*垂直居中*/
    align-items: center;
    /*水平居中*/
    justify-content: center;
}
.child{
    width: 30%;
    height: 30%;
}
```
```html
<div class="parent">
    <div class="child">

    </div>
</div>
```
#### 使用伪元素实现水平垂直居中
原理：不是很清楚
出自：[:after伪类+content内容生成经典应用举例](http://www.zhangxinxu.com/wordpress/2010/09/after%E4%BC%AA%E7%B1%BBcontent%E5%86%85%E5%AE%B9%E7%94%9F%E6%88%90%E5%B8%B8%E8%A7%81%E5%BA%94%E7%94%A8%E4%B8%BE%E4%BE%8B/)
优点：兼容性好
```css
.parent{
    width: 100%;
    height: 100%;
    /*水平居中*/
    text-align: center;
}
.parent:after{
    content: "";
    height: 100%;
    display: inline-block;
    vertical-align: middle;
}
.child{
    width: 50%;
    height: 50%;
    vertical-align: middle;
    display: inline-block;
}
```
```html
<div class="parent">
    <div class="child">
        
    </div>
</div>
```
#### 使用flex+align-items+justify-content实现水平垂直
优点：可以只修改父容器的`align-items`属性，实现子元素垂直方向的左中右居中
缺点：兼容性不好
```css
.parent{
    display: flex;
    /*垂直居中*/
    align-items: center;
    /*水平居中*/
    justify-content: center;
}
.child{
    width: 30%;
    height: 30%;
}
```
```html
<div class="parent">
    <div class="child">

    </div>
</div>
```
#### 使用padding+calc()实现
缺点：兼容性不好
```css
.parent{
    width: 300px;
    height: 300px;
    position: relative;
}
.child{
    border-width: 5px;
    width: 100px;
    height: 100px;
    background: red;
    padding: -webkit-calc((100% - 100px)/2);
    padding: -moz-calc((100% - 100px)/2);
    padding: calc((100%- 100px)/2);
    background-clip: content-box;
}
```
```html
<div class="parent">
    <div class="child">
        child
    </div>
</div>
```








