# Git使用手册

## 1.git仓库创建

git init/git add/git commit/ls/dir

1. 新建一个文件夹，在里面git bash,**git init**，这个文件夹就是一个仓库

   ```
   $ git init
   Initialized empty Git repository in D:/GitDemo/.git/
   ```

2. 没找到的话，就ls -ah，这个目录默认隐藏

3. 使用vscode编写一个文件到此仓库，写完之后使用**git add**

   ```
   $ git add readme.txt
   ```

4. **git commit**告诉Git，文件提交到仓库

   ```
   $ git commit -m "wrote a readme file"
   [master (root-commit) 812e6c2] wrote a readme file
    1 file changed, 2 insertions(+)
    create mode 100644 readme.txt
   ```

   -m "xxx"后面的是本次提交的说明，提交成功会显示以上内容

5. ls，dir可以查看当前目录下文件

6. 可以先添加很多文件，之后一次commit提交上去



## 2.版本

### git status/git diff

> 把文件修改后，使用**git status**查看结果

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

显示readme.txt被修改了，未提交

这个命令可以查看仓库当前状态



> **git diff**可以查看上次怎么修改的文件

```
$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index 084d42e..37bbe8d 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system
+Git is a distributed version control system
 Git is a free software
\ No newline at end of file
```

中间显示了做了什么修改

可以继续git add，git commit -m "xxx"



> git log查看版本

```
$ git log
commit a1b603d31c414c1c9f09e2ae2456a887adcb96c4 (HEAD -> master)
Author: galahad <3099229413@qq.com>
Date:   Mon Aug 7 20:29:10 2023 +0800

    append GPL

commit f5a307afeb0da7a71a1efff15e4f313b5a305b00
Author: galahad <3099229413@qq.com>
Date:   Mon Aug 7 20:26:02 2023 +0800

    add distributed

commit 812e6c2e1a812700b59aad90468b5799369ad47b
Author: galahad <3099229413@qq.com>
Date:   Mon Aug 7 20:05:03 2023 +0800

    wrote a readme file
```

最上面的是最新的提交

加上参数--pretty=oneline，前面的是commit id，后面是提交时写的备注

```
$ git log --pretty=oneline
a1b603d31c414c1c9f09e2ae2456a887adcb96c4 (HEAD -> master) append GPL
f5a307afeb0da7a71a1efff15e4f313b5a305b00 add distributed
812e6c2e1a812700b59aad90468b5799369ad47b wrote a readme file
```

> **git reset**

HEAD^表示上一个版本

--hard也是一个参数

```
$ git reset --hard Head^
HEAD is now at f5a307a add distributed
```

```
$ git reset --hard a1b60
HEAD is now at a1b603d append GPL
```

如果1->2->3;从3恢复到2版本，现在只有1->2版本，此时复制之前log出的3版本的前5位，使用reset就可以恢复；不过此时head指向就换了一下

> cat 

```
$ cat readme.txt
Git is a distributed version control system
Git is a free software
```

直接cat查看文件

> git reflog

```
$ git reflog
a1b603d (HEAD -> master) HEAD@{0}: reset: moving to a1b60
f5a307a HEAD@{1}: reset: moving to Head^
a1b603d (HEAD -> master) HEAD@{2}:  
f5a307a HEAD@{3}: commit: add distributed
812e6c2 HEAD@{4}: commit (initial): wrote a readme file
```

查看每次对应的



## 工作区和暂存区

Working Directory

电脑中可以看到的目录比如上面创建的gitdemo文件



.git是版本库

git版本库存的最重要的stage(又名index)的暂存区

还有Git创建的第一个分支master，指向master的指针HEAD

> 添加

1. git add把文件添加到暂存区
2. git commit提交更改，把暂存区所有内容提交到当前分支

> 恢复内容

**git checkout** -- file

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

> 删除

rm file

执行后会放在暂存区

执行commit

```
$ git commit -m "remove test.txt"
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

但是想还原，可以git checkout -- file