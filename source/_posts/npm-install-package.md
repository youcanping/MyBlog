---
title: NPM安装包
toc: true
comments: true
date: 2018-03-30 15:33:45
tags:
- NPM
categories:
- NPM
---

## NPM安装包
* 安装命令行工具一般用全局安装`npm install -g <package>`
* 安装某个模块到本地`npm install webpack`，一般用`require('webpack')`引入

### 全局安装
* `npm install -g 模块名`

#### 全局安装权限问题
全局安装一般都会遇到`permission denied`的报错，提示没有访问权限

#####  解决方法
1. `sudo npm install -g <package>`，以管理员身份运行

```bash
> sudo npm install -g webpack-cli
```
2. `sudo chown -R npm所在目录/{lib/node_modules,bin,share}`
官方推荐的做法，chown全称为change owner，即将npm目录的所有者指定为你的名字（授予权限），-R表示对指定目录下所有的子目录和文件也都采取同种操作。
> 通过`npm config get prefix`获取所在目录的路径

```bash
➜  ~ npm config get prefix
/usr/local
➜  ~ sudo chown -R youcanping /usr/local/{lib/node_modules,bin,share}
Password:
➜  ~ npm install -g webpack-cli
```

## 本地安装
### 安装生产环境依赖包
> `npm install --save <package>`

```bash
➜  ~ npm install --save loadsh
```

### 安装开发环境依赖包
> `npm install --save-dev <package>`或`npm install -D <package>`

```bash
➜  ~ npm install --save-dev webpack
```

* 示例

```json
 {
    "devDependencies": {
        "babel-core": "^6.26.0",
        "babel-loader": "^7.1.4",
        "babel-plugin-transform-runtime": "^6.23.0"
    }
 }
```

## NPM卸载包
### 卸载全局包
```
npm uninstall -g <package>
```
### 删除本地包
npm uninstall <package>

```
删除本地模块时你应该思考的问题：是否将在package.json上的相应依赖信息也消除？
npm uninstall 模块：删除模块，但不删除模块留在package.json中的对应信息
npm uninstall 模块 --save 删除模块，同时删除模块留在package.json中dependencies下的对应信息
npm uninstall 模块 --save-dev 删除模块，同时删除模块留在package.json中devDependencies下的对应信息
```

## 利用NPM发布包
> 如果`NPM`设置的淘宝源需要修改回来，具体操作看我上一篇博文

1. 添加用户
> 添加用户名，输入密码和邮箱

```bash
~ npm adduser
```

2. 登录
> 已经添加过用户的，下次发布需要登录下
```bash
~ npm login
```

3. 发布
* 包的名称和版本就是你项目里package.json里的name和version
* 包的名称不能和NPM已有的包重名
* 包名不能有大写字母/空格/下滑线
* publish之前要查看package.json文件里的main指定的路径，一定要写成dist/xxx.js或者dist/xxx.min.js，否则会报找不到依赖的错误
* 记得在package.json中更新我们的版本号，如果版本号相同的话会发布失败。

```bash
~ npm publish
```

### npm的版本控制
####  对于"version":"x.y.z"
1. 修复bug,小改动，增加z
2. 增加了新特性，但仍能向后兼容，增加y
3. 有很大的改动，无法向后兼容,增加x

#### 自动改变版本
> 通过npm version <update_type>, update_type为patch, minor, or major其中之一，分别表示补丁，小改，大改

* `major`对应的`X`，标识大改
* `minor`对应的`Y`，标识小改
* `patch`对应的`Z`，标识补丁




