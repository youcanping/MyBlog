---
title: js变量空值校验
toc: true
comments: true
date: 2017-12-20 16:53:16
tags: 变量校验
categories: JAVASCRIPT
---

### js判断变量空值的方法有
#### 使用表达式
- 使用表达式空值判断有个弊端就是，如果改变量没有声明，则页面报错。
![](http://our9i4zgx.bkt.clouddn.com/Snip20171221_17.png)

```javascript
if(!a){
    //如果a不为空 ...
}else {
    // 如果a为空 ...
}
//或者
var temp = a||"默认值";
```
- 用于函数内行参的判断，不会报错
```javascript
function sum(a,b) {
    var _a = a || 0;
    var _b = b || 0;
    return _a + _b;
}
```
### 安全的变量校验
- 如何对一个未知变量做判断呢，使用typeof判断一个没有声明的变量不会报错，返回'undefined'
```javascript
if(typeof a === 'undefined'){
    
}
```
![](http://our9i4zgx.bkt.clouddn.com/Snip20171221_19.png)