---
title: input事件中文输入优化
toc: true
comments: true
date: 2018-05-06 23:57:07
tags:
- COMPOSTIONSTART
- COMPOSTIONEND
- INPUT
categories:
- HTML5
- JAVASCRIPT
---

我们在处理input输入框实时输入状态时，一般都是绑定`input`事件，但是在中文输入法下，会出现拼音在输入框中也会触发`input`事件，并不是我们选择完汉子后触发输入事件，出现这种bug在某些应用场景就显得不那么优化，如根据用户输入内容实时查询信息，输入框中的拼音并不是我们想要查询的关键字，那如何只在用户选择汉子后触发`input`事件呢？         
最近在看`Vue.js`的`input`使用`v-model`指令时，就解决了中文输入法的问题。     
   
### 解决思路
使用`compositionstart`和`compositionend`,来处理中文输入问题。
* `compositionstart`：当浏览器有非直接的文字输入时, `compositionstart`事件会以同步模式触发。
* `compositionend`：当浏览器是直接的文字输入时, `compositionend`会以同步模式触发。

### 传统解决思路
```html
<input type="text" id="name" />
```
```js
    var node = document.querySelector('#name');
    var cpLock = false;
    node.addEventListener('compositionstart', function(){
        cpLock = true;
    })
    node.addEventListener('compositionend', function(){
        cpLock = false;
        if(!cpLock) console.log(this.value);
    })
    node.addEventListener('input', function(){
        if(!cpLock) console.log(this.value);
    });
```

### Vue.js的解决思路
```html
<input type="text" id="name" />
```
```js
var node = document.querySelector('#name');
 node.addEventListener('compositionstart', function (e) {
        e.target.composing = true;
    });
    node.addEventListener('compositionend', function (e) {
       if(!e.target.composing){return false}
       e.target.composing = false;
        trigger(e.target, 'input');
    });
    node.addEventListener('input', function (e) {
        if(e.target.composing){
            return false;
        }
        document.getElementById("show_name").innerHTML = e.target.value;
    });
    function trigger(el, type) {
        var e = document.createEvent('HTMLEvents');
        e.initEvent(type, true, true);
        el.dispatchEvent(e);
    }
```