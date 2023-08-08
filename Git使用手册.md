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



## 3.工作区和暂存区

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



## 4.上传到github

> 选择本地已有的文件，作为仓库

1. 在github里创建一个repository，写上仓库名

2. 在这个仓库下面可以看到提示信息，这里建议使用ssh连接，

3. ```
   git remote add origin git@github.com:michaelliao/learngit.git
   ```

   下面的是仓库连接地址

4. git remote(查看远程仓库) git branch -a(查看所有分支包括本地分支和远程分支) git branch -r(查看远程分支)

5. 之后git push origin master，可能显示没有这个分支，可以使用git branch查看分支，还可以添加分支**git branch branchname**(branchname是自己命名的)

6. 删除连接仓库git remote rm origin 删除分支git push origin --delete [branch_name]

> 配置ssh

没配置好ssh，连接不上

1. 查看密钥

   ```
   $ ls ~/.ssh
   id_ed25519      known_hosts
   id_ed25519.pub  known_hosts.old
   ```

2. 新生成密钥

   ```
   ssh-keygen -t ed22519 -C "email@example.com"
   ```

3. 使用默认，再ls ~/.ssh，pub是公钥，没有pub是私钥

4. 使用cat ~/.ssh/id_ed25519.pub

   出现的ssh-xxx复制到github设置的ssh-key中起个名字就好了



> 克隆仓库

在github创建一个仓库，选择一下add a readme在本地克隆

在本机找一个文件夹

```
$ git clone git@github.com:CHENCHENISHU/Gitskill.git
Cloning into 'Gitskill'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reus
Receiving objects: 100% (3/3), done.
```



## 5.分支

首先git有一个大分支master(就是一个指针指向当前最新的commit)，每次commit更新就是master动，head指向master动；

创建一个分支就是创建一个指针dev，指向最新进度，head也指向dev，dev动，head动，master不动，最后好几个分支合并成一个新的master，head再指向master

> 创建分支

```
$ git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：

```
$ git branch dev(创建分支)
$ git checkout dev(切换分支)
Switched to branch 'dev'
```

查看当前分支

```
$ git branch
*dev
 main
```

现在添加提交后，切换成master找不到添加的内容，因为那个提交在dev分支上

切换为dev分支，把成果合并到main分支

此时要切换到主分支，

使用

```
$ git merge dev
Updating c6f77b2..dc07127catc
Fast-forward
 README.md | 6 +++++-
 1 file changed, 5 insertions(+), 1 deletion(-)
```

合并成功，此时删除dev分支

```
$ git branch -d dev
Deleted branch dev (was dc07127).
```

| 作用               | 命令                                             |
| ------------------ | ------------------------------------------------ |
| 查看               | git branch                                       |
| 创建               | git branch <name>                                |
| 切换               | git checkout <name>`或者`git switch <name>       |
| 创建加切换         | git checkout -b <name>`或者`git switch -c <name> |
| 合并分支到当前分支 | git merge <name>                                 |
| 删除分支           | git branch -d <name>                             |

### 解决冲突

假如我们在同一个文件中不同分支做了不同修改，合并时就会发生冲突，此时要手动解决冲突

用`git log --graph`命令可以看到分支合并图。

### 分支管理

```
git merge --no-ff -m "merge with no-ff" test1(加入--no-ff可以用普通模式合并，合并后的历史有分支)
```

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

### bug分支

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

### Feature分支

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

### 多人协作

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。



## 6.标签

```
$ git tag v1.0
```

就是对当前的版本打了个标签

如果要对之前的版本打标签

获取

```
$ git log --pretty=oneline --abbrev-commit
```

> 打标签

```
$ git tag v0.9 c6f77b2
```

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。

> 删除标签

- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。
