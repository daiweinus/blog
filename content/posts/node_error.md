---
title: "env: node: No such file or directory macOS 解决方法"
date: 2021-11-10T12:37:00+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Bug
---

使用nmp命令时报错

```java
env: noder: No such file or directory
```

网上冲浪得到的解决方案

1. uninstall and reinstall Node.js
2. execute this command to create a link for node : sudo ln -s /usr/bin/nodejs /usr/local/bin/node

我用的方案1 重装 node.js 有效， 方案2 会报错。

```java
$ brew uninstall node
$ brew update
$ brew upgrade
$ brew cleanup
$ brew install node
$ brew link --overwrite node // 如果报错可跑此命名:$ brew unlink node && brew link node
$ brew postinstall node
$ node -v //能看到版本号就可以正常使用了
  v17.0.1
```

