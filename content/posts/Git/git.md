---
title: "git,github & gitlab"
date: 2021-11-14T16:24:04+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Git
---

**[Git](https://git-scm.com/)** 诞生于2005年，由大神 [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds) 开发的免费开源的分布式版本控制系统,可让你管理和跟踪源代码历史记录。Git 安装和维护在您的本地系统上，不需要internet联网。

github，和gitlab都是基于git开发的管理托管服务。其他 Git 存储库托管服务还有：BitBucket， SourceForge.

**[Github](https://github.com/)** 发布于2008年，是一种基于云的git仓库托管服务。提供免费的公共仓库(代码会被所有人看到)和收费的私有仓库(代码仅自己可见)。**通常用于托管开源项目**。

**[GitLab](https://about.gitlab.com/)** 发布于2013年，是一个基于 Web 的DevOps生命周期工具，它提供Git 存储库管理器。和GitHub相比gitlab允许免费创建私有仓库。 另外 gitlab还可以部署到本地服务器上，让开发团队对他们的代码仓库拥有更多的控制。**多用于企业或者个人的代码托管库**。

![Git: Reference Sheet – NeSI Support](https://support.nesi.org.nz/hc/article_attachments/360004194235/Git_Diagram.svg)

----

### Git 常用command：

![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5ydWFueWlmZW5nLmNvbS9ibG9naW1nL2Fzc2V0LzIwMTUvYmcyMDE1MTIwOTAxLnBuZw?x-oss-process=image/format,png)

**`git init` 初始化，在本地仓库创建 .git 文档**

```java
$ git init
Initialized empty Git repository in /gittest/.git/

// 查看.git隐藏目录里的本地库管理文件
$ ls -lA .git/
total 24
-rw-r--r--   1 user  staff   23  9 Nov 17:38 HEAD
-rw-r--r--   1 user  staff  137  9 Nov 17:38 config
-rw-r--r--   1 user  staff   73  9 Nov 17:38 description
drwxr-xr-x  13 user  staff  416  9 Nov 17:38 hooks
drwxr-xr-x   3 user  staff   96  9 Nov 17:38 info
drwxr-xr-x   4 user  staff  128  9 Nov 17:38 objects
drwxr-xr-x   4 user  staff  128  9 Nov 17:38 refs
```

**`git config` 设置用户签名（通常只需要设置本地系统签名就足够了）**

```java
$ git config user.name dai //设置本地仓库签名
$ git config user.email wdai@mail.com
$ cat .git/config //打开配置文件
[user]
	name = dai
	email = wdai@mail.com
$ git config --global user.name dai_glb //设置本地系统系统签名  
$ git config --global user.email wdai_glb@mail.com
$ cd ~ //返回根目录
$ pwd //显示路径
/Users/daiwei
$ cat .gitconfig
[user]
	name = dai_glb
	email = wdai_glb@mail.com
```

**`git status` 查看当前本地仓库状态**

```java
$ git status 
On branch master // 位于master branch

No commits yet // 本地仓库无提交记录

nothing to commit (create/copy files and use "git add" to track) // 暂存区也无可提交记录

$ cat > test.txt // 创建新txt文件，也可以用 $ touch test.txt
  test //输入文本 ctrl + D 保存并退出文本输入

$ git status
On branch master

No commits yet

Untracked files: // 未被git追踪文件
  (use "git add <file>..." to include in what will be committed)

	test.txt

nothing added to commit but untracked files present (use "git add" to track)
```

**`git add` 添加需要提交的文件**

```java
$ git add test.txt // $ git add . 添加所有被修改过的文件
$ git status
On branch master

No commits yet

Changes to be committed: // 追踪到已新committed文件
  (use "git rm --cached <file>..." to unstage) // git rm --cached <file> 可撤回当前操作

	new file:   test.txt // 新 added 文件
```

**`git rm --cached <file>`  撤回之前添加的文件**

```java
$ git rm --cached test.txt 
rm 'test.txt'
$ git status 
On branch master

No commits yet

Untracked files: // test.txt 回复为未被git追踪文件
  (use "git add <file>..." to include in what will be committed)

	test.txt

nothing added to commit but untracked files present (use "git add" to track)
```

**`git commit -m [message]` 提交添加的文件和备注信息**

```java
$ git add test.txt
$ git commit -m 'my first commit'
[master (root-commit) 91151c2] my first commit
 1 file changed, 1 insertion(+) //一个文件被改变，新增一行代码
 create mode 100644 test.txt
  
$ git status // 查看本地仓库状态
On branch master
nothing to commit, working tree clean // 无文件需要提交，工作区是干净的
```

**nano 修改test.txt文件内容**

```java
$ nano test.txt // 用nano editor 修改文件内容， ctrl + X 保存并退出
$ cat test.txt // 查看文件内容
test hello world  
$ git status // 查看文件被修改后在本地仓库的状态
On branch master //位于master branch
Changes not staged for commit: // 有改变但为commit
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   test.txt  //修改过的的文件：file—name
// 已added过，又被修改的文件可以直接 commit -a
no changes added to commit (use "git add" and/or "git commit -a")  
    
$ git add test.txt // add 被修改过的文件
$ git commit -m 'first time edit' // 提交 commit
[master 014b9c9] first time edit
 1 file changed, 1 insertion(+), 1 deletion(-) // 1个文件被修改过
$ git status
On branch master
nothing to commit, working tree clean // working tree OK
```

**`git log` 版本提交日志**

```java
$ git log
commit d77465cc8824b3f312740676c93f75f4be4370a9 (HEAD -> master) 
  //HEAD相当于一个指针，指向当前版本。我们切换版本相当于移动 HEAD指针
Author: dai <wdai@mail.com>
Date:   Wed Nov 10 12:21:17 2021 +0800

    add more text

commit 014b9c9d8287da50bd521950c889c147205610a2
Author: dai <wdai@mail.com>
Date:   Tue Nov 9 19:43:25 2021 +0800

    first time edit
  
$ git log --pretty=oneline // 当日志太多可以使用参数每次commit只显示一行
b963c9146d3fac75a6488c1885431dce0d60717d (HEAD -> master) add more test 3
219dc6b24eb17613bf6cd7621421e1e9e5975027 add more test 2
46a3927da53bfdcc8a7730fb042605b650be52f2 add more test 1
d77465cc8824b3f312740676c93f75f4be4370a9 add more text
014b9c9d8287da50bd521950c889c147205610a2 first time edit
91151c2bc99fb6184ed82bf7b8b5fc32d7118909 my first commit

$ git log --oneline // 只显示当前版本以及之后的版本，不显示前面的版本。哈希值只显示尾部，更加简短。     
b963c91 (HEAD -> master) add more test 3
219dc6b add more test 2
46a3927 add more test 1
d77465c add more text
014b9c9 first time edit
91151c2 my first commit
  
$ git reflog  // 显示所有版本，推荐使用
b963c91 (HEAD -> master) HEAD@{0}: commit: add more test 3 // HEAD 0 当前版本
219dc6b HEAD@{1}: commit: add more test 2 // HEAD 1，到此版本需要移动指针一次
46a3927 HEAD@{2}: commit: add more test 1
d77465c HEAD@{3}: commit: add more text
014b9c9 HEAD@{4}: commit: first time edit
91151c2 HEAD@{5}: commit (initial): my first commit
```

**`git-reset` : Reset current HEAD to the specified state  重置当前HEAD指针到指定版本**

```java
git reset --soft : not touch the index file or the working tree at all.//仅重置本地库。
git reset --mix : resets the index but not the working tree.//重置本地库和暂存库。
git reset --hard : resets the index and working tree.//重置本地库，暂存区，工作库。
git reset --merge :
git reset --keep : 
git-revert(1) : //重置最新版本，返回上一个版本
```

**`git reset --hard [hash_valve]` 基于索引值前进后退版本，推荐使用**

```java
$ git reflog // 显示各版本信息
a6070ce (HEAD -> master) HEAD@{0}: reset: moving to a6070ce
4a34a05 HEAD@{1}: reset: moving to 4a34a05
a6070ce (HEAD -> master) HEAD@{2}: commit: add 333
9143841 HEAD@{3}: commit: add 222
4a34a05 HEAD@{4}: commit: add 111
b963c91 HEAD@{5}: commit: add more test 3
219dc6b HEAD@{6}: commit: add more test 2
46a3927 HEAD@{7}: commit: add more test 1 // 目标版本索引值 46a3927
d77465c HEAD@{8}: commit: add more text
014b9c9 HEAD@{9}: commit: first time edit
91151c2 HEAD@{10}: commit (initial): my first commit
$ cat test.txt //显示当前版本内容
111
222
333
$ git reset --hard 46a3927 // 基于索引值退回到目标版本
HEAD is now at 46a3927 add more test 1 //版本回退成功
$ cat test.txt //显示目标版本内容
test hello world
1111dwd dwdd
adad
add more1
```

**`git reset --hard HEAD^` 基于 ^ 异或符号的 版本回退， 只可以回退，不可以前进，不推荐**

```java
$ git log --oneline  // 单行显示log
a6070ce (HEAD -> master) add 333
9143841 add 222
4a34a05 add 111
b963c91 add more test 3
219dc6b add more test 2
46a3927 add more test 1
d77465c add more text
014b9c9 first time edit
91151c2 my first commit
$ git reset --hard HEAD^  //一个 ^ 回退一个版本
HEAD is now at 9143841 add 222
$ cat test.txt          
111
222
// $ git reset --hard HEAD^^^^ //四个^^^^ 回退四个版本
$ git reset --hard HEAD~4  // HEAD~4 == HEAD^^^^
HEAD is now at 46a3927 add more test 1
$ cat test.txt             
test hello world
1111dwd dwdd
adad
add more1
```

**恢复已删除文件**

```java
$ nano aaa.txt // 工作区新建文件aaa.txt
$ ls
aaa.txt		test.txt
  
$ git add aaa.txt // 添加并提交新建文件到本地仓库
$ git commit -m 'add aaa.txt'
[master e377c41] add aaa.txt
 1 file changed, 1 insertion(+)
 create mode 100644 aaa.txt
$ git log --oneline // 查看log
e377c41 (HEAD -> master) add aaa.txt // 当前版本已添加新文件
a6070ce add 333
9143841 add 222
4a34a05 add 111
b963c91 add more test 3
219dc6b add more test 2
46a3927 add more test 1
d77465c add more text
014b9c9 first time edit
91151c2 my first commit
  
$ rm aaa.txt // remove 工作区新建的文件
$ ls 
test.txt
  
$ git status //查看 git 暂存区当前状态
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    aaa.txt // 显示已删除但还未提交本地仓库

no changes added to commit (use "git add" and/or "git commit -a")
   
$ git add aaa.txt //添加删除请求
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage) // reset 可返回删除前版本

	deleted:    aaa.txt 

$ git commit -m 'delete aaa.txt' // 提交删除请求
[master a3c257a] delete aaa.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 aaa.txt
$ git status // 查看暂存区状态，clean
On branch master
nothing to commit, working tree clean
    
$ git log --oneline //查看日志
a3c257a (HEAD -> master) delete aaa.txt //当前版本
e377c41 add aaa.txt //新建文件版本
a6070ce add 333
9143841 add 222
4a34a05 add 111
b963c91 add more test 3
219dc6b add more test 2
46a3927 add more test 1
d77465c add more text
014b9c9 first time edit
91151c2 my first commit
$ ls // ls -l 可查看文件信息
test.txt   

$ git reset --hard e377c41 //恢复删除之前版本
HEAD is now at e377c41 add aaa.txt
¥ ls // 查看文件aaa.txt 已恢复
aaa.txt		test.txt
```

**`git diff [file]` 比较文件差异**

```java
// diff 不仅可以和工作区文件进行比较，还可以和暂存区，本地库之前各文件进行比较
$ git diff aaa.txt 
diff --git a/aaa.txt b/aaa.txt
index 41cfa54..e452369 100644
--- a/aaa.txt 
+++ b/aaa.txt
@@ -1 +1,3 @@
 crated for delete testing
+addd // +表示新增行
+addd // +表示新增行
```

## `git branch`

```java
$ git branch -v // 产看全部分支
* master 01c9112 edit aaa.txt
  
$ git branch hot_fix // 创建新的分支
$ git branch -v
  // 此时版本hash值是一样的 01c9112，说明分支和master处于同一个版本
  hot_fix 01c9112 edit aaa.txt 
* master  01c9112 edit aaa.txt // * 表示现在目前坐在分支
  
$ git checkout hot_fix // 切换分支
Switched to branch 'hot_fix'
$ git branch -v       
* hot_fix 01c9112 edit aaa.txt  // 分支切换到 * hot_fix
  master  01c9112 edit aaa.txt
  
$ nano test.txt // 在 hot_fix分支上修改 test.txt文件
$ git add test.txt //提交修改
$ git commit -m 'edit test.txt by hot_fix'
[hot_fix e2b708c] edit test.txt by hot_fix
 1 file changed, 1 insertion(+)
$ git branch -v 
  //查看分支发现新分支和master的 hash值 已经不一样了，说明分支版本已跟新
* hot_fix e2b708c edit test.txt by hot_fix
  master  01c9112 edit aaa.txt
  
// 合并分支前，要先切换到你想要跟新的分支上，比如你想把hot_fix分支合并到master分支，就需要先切换到master分支，再把hot_fix分支合并进来。 
$ git checkout master
Switched to branch 'master'
$ git branch
  hot_fix
* master  // 切换到meter分支
$ git merge hot_fix // 把hot_fix分支 合并到 master分支
Updating 01c9112..e2b708c
Fast-forward
 test.txt | 1 +
 1 file changed, 1 insertion(+)
$ cat test.txt //查看文件，合并成功
111
222
333
444 add by hot_fix //这一行是hot_fix分支修改后合并到master的

$ git branch -v //合并完成后分支和master hash值一样 e2b708c
  hot_fix e2b708c edit test.txt by hot_fix
* master  e2b708c edit test.txt by hot_fix

//处理合并冲突conflict
$ nano test.txt //在master修改文件
$ git add test.txt
$ git commit -m 'add 555 by master'
[master 154943a] add 555 by master
 1 file changed, 2 insertions(+), 1 deletion(-)
$ git checkout hot_fix //切换到hot分支再修改文件
Switched to branch 'hot_fix'
$ nano test.txt
$ git add test.txt
$ git commit -m 'add 666 by hot_fix'
[hot_fix f22571f] add 666 by hot_fix
 1 file changed, 1 insertion(+)
$ git merge master // 合并冲突
Auto-merging test.txt
CONFLICT (content): Merge conflict in test.txt
Automatic merge failed; fix conflicts and then commit the result.  

$ cat test.txt //查看文件会发现 git 在文件内有标记conflict的位置
111
222
333
<<<<<<< HEAD  
444 add by hot_fix 
666 add by hot_fix
=======
444 add by hot_fix
555 add by master 
>>>>>>> master

$ nano test.txt //修改冲突
$ git status //查看状态
On branch hot_fix
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   test.txt //所有冲突都被修改

no changes added to commit (use "git add" and/or "git commit -a")
$ git add test.txt //添加修改
$ git status      
On branch hot_fix
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   test.txt //修改完成

$ git commit -m 'resolve conflict' //提交修改
[hot_fix 7da1a5d] resolve conflict
$ git status  //clean
On branch hot_fix
nothing to commit, working tree clean
$ git branch -v
* hot_fix 7da1a5d resolve conflict
  master  154943a add 555 by master
$ cat test.txt
111
222
333
444 add by hot_fix
555 add by master

```

## Github

### 新建本地工作文件夹并提交到git本地仓库

```java
$ cd githubtest
$ git init
Initialized empty Git repository in /Users/daiwei/Desktop/githubtest/.git/
$ nano test.txt
$ cat test.txt
test 1 3 3
$ git add test.txt
$ git commit -m 'test github'
[master (root-commit) fca7556] test github
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```

### git remote add

```java
$ git remote -v // 没有添加远程仓库之前， -v　是空的没有东西显示
$ git remote add origin https://github.com/daiweinus/githubtest.git 
$ git remote -v // 添加远程仓库之后， -v 可见远程仓库地址了
origin	https://github.com/daiweinus/githubtest.git (fetch)
origin	https://github.com/daiweinus/githubtest.git (push)
```

### git push

```java
$ git push origin master // push到你的远程仓库 master 分支上
Username for 'https://github.com': yourusername
Password for 'https://yourusername@github.com': yourPAT [personal access token]
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 217 bytes | 217.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/yourusername/githubtest.git
 * [new branch]      master -> master
```

### git clone

```java
$ git clone https://github.com/yourusername/githubtest.git
Cloning into 'githubtest'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
  
yanqin@35 github_clone % ls  // 1.clone完成后远程仓库文件已下载到本地仓库
githubtest
$ cd githubtest
$ ls
test.txt
$ ls -lA
total 8
drwxr-xr-x  12 yanqin  staff  384 15 Nov 12:20 .git // 2.clone会自动初始化本地git仓库
-rw-r--r--   1 yanqin  staff   11 15 Nov 12:20 test.txt
$ git remote -v // 3.clone会自动帮本地仓库添加远程仓库
origin	https://github.com/yourusername/githubtest.git (fetch)
origin	https://github.com/yourusername/githubtest.git (push)
```

### git fetch 拉取

```java
$ git fetch origin master // 
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/yourusername/githubtest
 * branch            master     -> FETCH_HEAD
   fca7556..0495c81  master     -> origin/master
   
$ cat test.txt // fetch后本地工作区文件并未改变
test 1 3 3
$ git checkout origin/master //查看本地git仓库
Note: checking out 'origin/master'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 0495c81 clone push test
$ cat test.txt // fetch只是把远程仓库文件下载到了本地git仓库
test 1 3 3
github_clone 1 2 3
```

### git merge 合并

git merge vs git merge --no-ff 后者创建一个新的合并提交，让代码维护更加容易。

![git merge --no-ff 和 git merge 的区别](https://i.stack.imgur.com/GGkZc.png)

```java
$ git status 
On branch master
nothing to commit, working tree clean
$ git merge origin/master // 
Updating fca7556..0495c81
Fast-forward
 test.txt | 1 +
 1 file changed, 1 insertion(+)
$ cat test.txt // merge完成后，工作区test文件已修改同步完成
test 1 3 3
github_clone 1 2 3
```

### git pull = fetch + merge

```java
$ cat test.txt
test 1 3 3
github_clone 1 2 3
  
$ git pull origin master //
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/daiweinus/githubtest
 * branch            master     -> FETCH_HEAD
   0495c81..ad5056c  master     -> origin/master
Updating 0495c81..ad5056c
Fast-forward
 test.txt | 1 +
 1 file changed, 1 insertion(+)
   
$ cat test.txt // pull = fetch + merge
test 1 3 3
github_clone 1 2 3
github_clone 4 5 6
```

### conflict

```java
$ cat test.txt // 原文件
test 1 3 3
github_clone 1 2 3
github_clone 4 5 6
$ nano test.txt // 在 master 仓库修改原文件
$ cat test.txt
test 1 3 3 by gihub_master //
github_clone 1 2 3
github_clone 4 5 6
$ git commit -m 'edit by github_master' test.txt //提交到本地仓库
[master 8d3e36c] edit by github_master
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git push origin master //push到远程仓库
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 293 bytes | 293.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/daiweinus/githubtest.git
   ad5056c..8d3e36c  master -> master
     
$ githubtest % cd .. 
$ Desktop % cd github_clone
$ github_clone % cd githubtest
$ githubtest % ls // 切换到clone 仓库， 
test.txt
$ nano test.txt
$ cat test.txt // 修改clone 仓库工作区文件
test 1 3 3 by github_clone
github_clone 1 2 3
github_clone 4 5 6
$ git commit -m 'test conflict' test.txt //提交到本地仓库
[master f8c19a2] test conflict
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git push origin master  // 也push到远程仓库
To https://github.com/daiweinus/githubtest.git 
 ! [rejected]        master -> master (fetch first) //push悲剧
error: failed to push some refs to 'https://github.com/daiweinus/githubtest.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again. //提示先pull before push
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  
$ git pull origin master // pull远处仓库
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/daiweinus/githubtest
 * branch            master     -> FETCH_HEAD
   ad5056c..8d3e36c  master     -> origin/master
Auto-merging test.txt
CONFLICT (content): Merge conflict in test.txt // 提示有conflict 
Automatic merge failed; fix conflicts and then commit the result.
$ nano test.txt //修改本地仓库冲突文件，去掉特殊符号，保留想要修改的内容
$ cat test.txt 
test 1 3 3 by github_clone
test 1 3 3 by gihub_master
github_clone 1 2 3
github_clone 4 5 6
$ git add test.txt //从新提交修改后的文件到本地仓库
$ git commit -m 'resolve conflict'
[master 9209bdb] resolve conflict
$ git status 
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
$ git push origin master // 再次从本地仓库push到远程仓库，无冲突
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 561 bytes | 561.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To https://github.com/daiweinus/githubtest.git
   8d3e36c..9209bdb  master -> master
```

### [SSH 免密码登陆设置](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```java
$ ssh-keygen -t ed25519 -C "your_email@example.com"
  
//Note: If you are using a legacy system that doesnt support the Ed25519 algorithm, use:
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

##### ssh-keygen : Secure Shell - key generate 

##### -t rsa : -type rsa 

rsa (**Rivest–Shamir–Adleman**) 最古老的非对称加密算法之一;  ed25519 **爱德华兹曲线数字签名算法**( **EdDSA** ) 是一种使用基于扭曲爱德华兹曲线的Schnorr 签名变体的数字签名方案，它旨在在不牺牲安全性的情况下比现有的数字签名方案更快。

ed25519加密解密很快,生成时间短而且安全性更高,rsa则加密解密稍慢,生成时间长,安全性没有ed25519高,只是rsa基本都是默认,所以用的人更多。

##### -b 4096 

b 指定密钥长度。对于RSA密钥，最小要求768位，默认是2048位。命令中的4096指的是RSA密钥长度为4096位。

##### -C : comment 添加注释

```java
githubtest $ cd ~ //返回更根目录
$ rm -r .ssh/  //删除旧的ssh加密文件
$ ssh-keygen -t ed25519 -C 6608118@gmail.com  // 生成新ssh加密文件        
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/username/.ssh/id_ed25519): //回车键，使用默认值
Created directory '/Users/daiwei/.ssh'.
Enter passphrase (empty for no passphrase): //回车键，使用默认值
Enter same passphrase again: //回车键，使用默认值
Your identification has been saved in /Users/username/.ssh/id_ed25519.
Your public key has been saved in /Users/username/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:ktMDqgSKDbWqUAdUd61n63+DZAgaoUEjtSLvg1e3FpU username@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
| .=+= . ..       |
| . +.+.. ..      |
|+ + oo..E.       |
|oO o...=o o      |
|= + o *oS+ o     |
|o+ o ..= .o o    |
|o =   o  . o .   |
| . . .    . . o  |
|           ... . |
+----[SHA256]-----+
$ cd .ssh
.ssh $ ls -lA
total 16
-rw-------  1 yanqin  staff  411 16 Nov 11:33 id_ed25519
-rw-r--r--  1 yanqin  staff   99 16 Nov 11:33 id_ed25519.pub
.ssh $ cat id_ed25519.pub //copy .pub 加密文件
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPyWgD16fGjNd/lPUwQ5AFTBNZ0SjKVi9hBw92YWemNi username@gmail.com
```

登陆github ->setting -> SSH and GPS keys -> New SSH key -> 将复制的.pub 文件粘贴保存。

![The key field](https://docs.github.com/assets/images/help/settings/ssh-key-paste.png)

```java
$ ssh -T git@github.com //测试 ssh 是否设置成功
The authenticity of host 'github.com (20.205.243.166)' cant be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes  
Warning: Permanently added 'github.com,20.205.243.166' (RSA) to the list of known hosts.
Hi username! Youve 'successfully' authenticated, but GitHub does not provide shell access.
  
githubtest $ git remote -v // 此时只有两个 https 远程仓库地址
origin	https://github.com/usernamegithubtest.git (fetch)
origin	https://github.com/username/githubtest.git (push)
githubtest $ git remote add origin_ssh git@github.com:daiweinus/githubtest.git
githubtest $ git remote -v // 复制添加ssh 远程仓库地址
origin	https://github.com/username/githubtest.git (fetch)
origin	https://github.com/username/githubtest.git (push)
origin_ssh	git@github.com:username/githubtest.git (fetch)
origin_ssh	git@github.com:username/githubtest.git (push)
  
githubtest $ git push origin_ssh master //使用ssh提交到远程仓库
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 619 bytes | 619.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:daiweinus/githubtest.git
   9209bdb..9878883  master -> master
```

Ref: https://blog.csdn.net/qq_42255991/article/details/102783991

