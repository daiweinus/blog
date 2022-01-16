---
title: "git : Changes not staged for commit"
date: 2021-11-16T17:19:26+08:00
draft: true
toc: false
images:
  - "images\totoro.jpeg"
tags: 
  - Git
---

```assembly
Changes not staged for commit:
	modified:   themes/hermit (modified content, untracked content)

no changes added to commit
```

出现此问题是因为该路径内有文件已修改但是没被提交到本地仓库，可以尝试 cd 到子文件路径，add & commit, 然后返回原工作区路径，再add & commit一次。

```java
$ cd themes/hermit
hermit $ git add .
hermit $ git git commit -m 'message'

hermit $ cd ../..
$ git add .
$ git git commit -m 'message'  
```

