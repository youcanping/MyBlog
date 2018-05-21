---
title: node-gyp error
date: 2017-12-17 20:24:15
tags: 
- hexo
categories: 
- node
toc: true
comments: true

---

### 报错信息
- 今天在安装hexo博客命令行工具是遇到一个问题，报错如下

```bash
youcanpingdeMacBook-Pro:MyBlog issuser$ sudo npm install hexo-cli -g

/usr/local/bin/hexo -> /usr/local/lib/node_modules/hexo-cli/bin/hexo

> fsevents@1.1.3 install /usr/local/lib/node_modules/hexo-cli/node_modules/fsevents
> node install

node-pre-gyp ERR! Tried to download(undefined): https://fsevents-binaries.s3-us-west-2.amazonaws.com/v1.1.3/fse-v1.1.3-node-v59-darwin-x64.tar.gz 
node-pre-gyp ERR! Pre-built binaries not found for fsevents@1.1.3 and node@9.3.0 (node-v59 ABI, unknown) (falling back to source compile with node-gyp) 
gyp ERR! clean error 
gyp ERR! stack Error: EACCES: permission denied, rmdir 'build'
gyp ERR! System Darwin 17.2.0
gyp ERR! command "/usr/local/bin/node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "clean"
gyp ERR! cwd /usr/local/lib/node_modules/hexo-cli/node_modules/fsevents
gyp ERR! node -v v9.3.0
gyp ERR! node-gyp -v v3.6.2
gyp ERR! not ok 
node-pre-gyp ERR! build error 
node-pre-gyp ERR! stack Error: Failed to execute '/usr/local/bin/node /usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js clean' (1)
node-pre-gyp ERR! stack     at ChildProcess.<anonymous> (/usr/local/lib/node_modules/hexo-cli/node_modules/fsevents/node_modules/node-pre-gyp/lib/util/compile.js:83:29)
node-pre-gyp ERR! stack     at ChildProcess.emit (events.js:159:13)
node-pre-gyp ERR! stack     at maybeClose (internal/child_process.js:943:16)
node-pre-gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:220:5)
node-pre-gyp ERR! System Darwin 17.2.0
node-pre-gyp ERR! command "/usr/local/bin/node" "/usr/local/lib/node_modules/hexo-cli/node_modules/fsevents/node_modules/node-pre-gyp/bin/node-pre-gyp" "install" "--fallback-to-build"
node-pre-gyp ERR! cwd /usr/local/lib/node_modules/hexo-cli/node_modules/fsevents
node-pre-gyp ERR! node -v v9.3.0
node-pre-gyp ERR! node-pre-gyp -v v0.6.39
node-pre-gyp ERR! not ok 
Failed to execute '/usr/local/bin/node /usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js clean' (1)
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.1.3 (node_modules/hexo-cli/node_modules/fsevents):
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.1.3 install: `node install`
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: Exit status 1

```

### 解决方法
- 解决方法，单独执行如下命令即可

```bash
sudo npm install -g node-gyp
```