---
title: JavaScript学习笔记-基本概念
toc: true
comments: true
date: 2018-05-21 15:20:26
tags:
- JavaScript
categories:
- JavaScript
- JavaScript学习笔记
---

## 标识符
所谓**标识符**，就是只变量、函数、属性名的名字，或者函数的参数。
标识符的组成规则：
 * 第一个字符必须是一个字母、下划线(_)或一个美元符号($);
 * 其他字符可以是字母、下划线、美元符号或数字。

> 按照惯例，ECMAScript标识符采用驼峰命名规则(Camel-Case)，一个单词字母小写其他单词首字母大写（小驼峰命名法），或全面单词首字母都大写（大驼峰命名法），构造函数建议采用大驼峰命名法。

```js
    var abc123 = "";
    var _temp = "";
    var $list = [];
    function User(name, age){};
````

## 数据类型
### ECMAScript5中有5种简单数据类型
|类型|值|
|:---|:----|
|Undefined  |  undefined|
|Null| null |
|Boolean| true,false|
|Number| 整数和小数|
|String| 'abc'|

### ECMAScript复杂数据类型
`Object`，是由一组**无序**的键值对组成。

## 类型检查
### typeof和constructor判断基本数据类型
| variable | typeof variable | variable.constructor |
|:---|:----|:----|
|`{an: "object"}`| `"object"` | `Object` |
|`["an", "array"]`| `"object"` | `Array` |
|`function(){}`| `"function"` | `Function` |
|`"a string"`| `"string"` | `String` |
|`89`| `"number"` | `Number` |
|`true`| `"boolean"` | `Boolean` |
|`new User()`| `"object"` | `User` |
|`null`| `"object"` | `报错` |
|`undefined`| `"undefined"` | `报错` |

* 对未初始化，未定义的变量使用`typeof`操作费返回`undefined`，可以利用这以特性安全的判断变量是否定义，否则使用未定义的变量会导致页面报错。
* `null`被认为是空对象的引用，使用`typeof`操作符返回`object`。
* 数组也是对象，`typeof`返回`object`。
* 当变量是`null`或`undefined`时，调用`constructor`会报错。

```js
    var type =  typeof 1; // "number"
```

### 使用instanceof操作符判断复杂数据类型
`instanceof` 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。
* [MDN instanceof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)

#### 语法
> object instanceof constructor
* object 要检测的对象
* constructor 某个构造函数

#### 示例
```js
function C(){};
var o = new C(){};
o instanceof C // true
```

## Undefined类型
* `Undefined`只有一个值`undefined`，未初始化的变量默认值就是`undefined`;
* 不需要显示声明一个变量的初始值为`undefined`;
* 使用`typeof`操作一个未定义的变量返回`undefined`;

```js
    var a;
    if(a !== undefined){
        // todo
    }
```

## Null类型
* `Null`类型只有一个值`null`，标识空对象的指针。
* 对定义的变量**将来**用于保存对象要显示初始化赋值`null`，有利于区分`null`和`undefined`;
* `undefined`值是派生自`null`，`==`测试返回`true`;

```js
    var obj = null;
    if(obj !== null){
         // todo
    }
```

















