---
title: 如何优雅的切换NPM源
toc: true
comments: true
date: 2018-03-30 13:59:57
tags:
- NPM
categories:
- NPM
---

## NPM使用淘宝镜像
我们在实际项目开发中难免会用到NPM，但由于国内网络访问国外NPM很慢，有的还存在下载失败的问题，这个时候很多人都会使用国内淘宝镜像，也就是淘宝源，但是使用淘宝源有个问题就是，当我们要在NPM发布库时，是需要切到国外的NPM源的。

## 设置淘宝源步骤
### 临时使用
```bash
➜  ~ npm --registry https://registry.npm.taobao.org install express
```

### 持久使用
```bash
➜  ~ npm config set registry https://registry.npm.taobao.org
```

* 验证是否配置成功

```bash
➜  ~ npm config get registry
https://registry.npm.taobao.org/
```

### 通过cnpm使用
```bash
➜  ~ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
* 使用

```bash
➜  ~ cnpm install express
```

## 手动删除淘宝源
```bash
➜  ~ npm config delete registry
```

## 使用nrm管理源
* [https://www.npmjs.com/package/nrm](https://www.npmjs.com/package/nrm)
### 安装nrm，MAC机器要加上sudo
```bash
➜  ~ npm install -g nrm
```
### 查看源列表
```bash
➜  ~ nrm ls

  npm ---- https://registry.npmjs.org/
  cnpm --- http://r.cnpmjs.org/
* taobao - https://registry.npm.taobao.org/
  nj ----- https://registry.nodejitsu.com/
  rednpm - http://registry.mirror.cqupt.edu.cn/
  npmMirror  https://skimdb.npmjs.com/registry/
  edunpm - http://registry.enpmjs.org/
```

### 切换源
```bash
➜  ~ nrm use npm
                         verb config Skipping project config: /Users/youcanping

   Registry has been set to: https://registry.npmjs.org/

➜  ~ nrm ls

* npm ---- https://registry.npmjs.org/
  cnpm --- http://r.cnpmjs.org/
  taobao - https://registry.npm.taobao.org/
  nj ----- https://registry.nodejitsu.com/
  rednpm - http://registry.mirror.cqupt.edu.cn/
  npmMirror  https://skimdb.npmjs.com/registry/
  edunpm - http://registry.enpmjs.org/
```

### 帮助说明
```bash
 ~ nrm -h

  Usage: nrm [options] [command]

  Options:

    -V, --version                输出版本号
    -h, --help                   输出使用信息

  Commands:

    ls                           列出所有源列表
    current                      显示当前源名称
    use <registry>               切换源
    add <registry> <url> [home]  添加一个自定义源
    del <registry>               删除一个自定义源
    home <registry> [browser]    使用可选浏览器打开源主页
    test [registry]              显示特定或所有源管理机构的响应时间
    help                         打印此帮助
```





