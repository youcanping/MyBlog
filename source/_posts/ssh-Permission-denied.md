---
title: 'ssh Permission denied '
toc: true
date: 2017-12-20 14:27:41
tags: hexo 
categories: node
comments: true
---

### 该问题对应的网上解决方式
* [segmentfault对应的该问题回答](https://segmentfault.com/q/1010000003061640/a-1020000012587308)
* [stackoverflow对该问题的回调](https://stackoverflow.com/questions/12940626/github-error-message-permission-denied-publickey)

### 问题描述

换电脑使用hexo发布博客，hexo源码是备份到github上的，clone到本地 hexo g 生成博客没有报错，hexo d发布博客出问题了，报出如下错误。

```bash
> sudo hexo d
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

    at ChildProcess.<anonymous> (/Users/youcanping/Desktop/MyBlog/node_modules/hexo-util/lib/spawn.js:37:17)
    at emitTwo (events.js:125:13)
    at ChildProcess.emit (events.js:213:7)
    at maybeClose (internal/child_process.js:927:16)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:211:5)

```

### 解决方式
1. 先看本地是否有ssh文件
```bash
> cd ~/.ssh
> ls
id_rsa          id_rsa.pub      known_hosts
```

2. 有则把公钥加到github
```bash
>cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDVRgHi3gPdBcQ... xxxx@163.com
```

3. github 添加公钥示意图
![](http://our9i4zgx.bkt.clouddn.com/Snip20171220_3.png)
![](http://our9i4zgx.bkt.clouddn.com/Snip20171220_4.png)
![](http://our9i4zgx.bkt.clouddn.com/Snip20171220_5.png)

4. 如果以上操作问题还不能解决,并且执行 ssh -T git@github.com 出现如下提示，说明本地公钥没有问题，则看第5步
```bash
> ssh -T git@github.com
Hi youcanping! You've successfully authenticated, but GitHub does not provide shell access.
```

5. 看本地的.git/config设置的仓库url地址和github使用的链接地址是否一致如下图,如use https,则url需要用https的仓库地址，我的就是这个问题。
![](http://our9i4zgx.bkt.clouddn.com/blog/Snip20171226_12.png)
```bash
> cat .git/config
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[remote "origin"]
        url = https://github.com/youcanping/MyBlog.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master

```

