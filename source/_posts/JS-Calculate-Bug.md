---
title: JS-Calculate-Bug
toc: true
comments: true
date: 2018-01-18 11:11:23
tags:
- JS CALCULATE
categories:
- JAVASCRIPT
---

> 我们在做JS浮点数计算的时候回出现各种奇怪的现象，出现精度问题，不是JS的问题，所有语言都有这个问题。

如
```bash
> 1.43 + 1.00 => 2.4299999999999997
> 2.2 - 1.9   => 0.30000000000000027
> 2.2 * 2.2   => 4.840000000000001
> 2.1 / 0.3   => 7.000000000000001
```
> 遇到这种问题，网上已有解决方案，既然js对小数的计算有问题，思路就是先转成整数计算，计算后再转成小数。
* [JavaScript 浮点数运算的精度问题](http://www.css88.com/archives/7340#more-7340)
* [js小数计算如何保证得到正确的值？](https://segmentfault.com/q/1010000000670650)
* [解决JavaScript数字精度丢失问题的方法](http://www.jb51.net/article/75801.htm)

> 对于金融类的推荐使用下面类库解决JS精度问题
* [https://github.com/josdejong/mathjs](https://github.com/josdejong/mathjs)
* [JavaScript 格式化数字、金额、千分位、保留几位小数、舍入舍去…](http://www.css88.com/archives/7324)