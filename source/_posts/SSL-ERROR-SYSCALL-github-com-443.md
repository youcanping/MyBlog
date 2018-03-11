---
title: SSL_ERROR_SYSCALL in connection to github.com:443
toc: true
comments: true
date: 2018-03-01 16:43:39
tags:
- GIT
- GITHUB
categories:
- GIT
---

# LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
## 在clone或者push远程仓库报错
报错信息如下：
```bash
Error: fatal: unable to access 'https://github.com/xxx/xxx.github.io.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443

    at ChildProcess.<anonymous> (/Users/xxx/workspace/MyBlog/node_modules/hexo-util/lib/spawn.js:37:17)
    at emitTwo (events.js:125:13)
    at ChildProcess.emit (events.js:213:7)
    at maybeClose (internal/child_process.js:927:16)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:211:5)

```
## 解决方法
* 把仓库链接地址由https修改为ssl的地址