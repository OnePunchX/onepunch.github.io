---
title: 一些好用的git命令
date: 2020-09-10 10:17:20
tags: git
categories: 前端
---

## git 代码版本管理工具

最开始的时候，只会 git add ,git commit , git push , git pull ,当熟练使用这样的提交代码的“硬”命令后
在工作中不断遇见各种情况，学习了各种好用的命令
也得益与我执着与手敲命令而不是用一些 git 工具
在这里做一个简单的总结，并再次拓宽自己的 git 知识～
冲鸭

### git stash

git stash 可以把所有未提交的修改（工作区和暂存区）也就是 git commit 之前的 ，保存到堆栈中，先进后出。
在日常敲代码，中经常会使用
在切分支，紧急上线，但是正在开发的功能分支还没有开发完的时候，就可以使用这个命令啦

#### git stash save "zhujunTest"

可以在暂存的时候加备注 理解为 git commit -m “” 这种备注即可

#### git stash list

查看当前 stash 中的内容

#### git stash pop

将当前 stash 中的内容弹出，并应用到当前分支对应的工作目录上。
注：该命令将堆栈中最近保存的内容删除（栈是先进后出）

#### git stash apply

将堆栈中的内容应用到当前目录，不同于 git stash pop，该命令不会将内容从堆栈中删除，也就说该命令能够将堆栈的内容多次应用到工作目录中，适应于多个分支的情况。
可以使用 git stash apply + stash 名字（如 stash@{1}）指定恢复哪个 stash 到当前的工作目录。

#### git stash clear

清除堆栈中的所有 内容

#### git stash show

查看堆栈中最新保存的 stash 和当前目录的差异。

### git rebase

本地代码多次提交后，合并主分支的时候，如果用 git merge 分支树会分叉
这时候使用 git rebase 就很酷很优雅
来吧展示

```
git checkout master
git pull origin master
git checkout 本地分支
git rebase master
// 如果有冲突，解决冲突 然后git add .    +   git rebase --continue
git checkout master
git merge 本地分支
git push

```

完事。

### git reset

重置 HEAD 指针

#### git reset --hard

比如 git reset --hard origin master 这时会清空暂存区，也就是说没有 commit 的内容都会被清除掉
重置位置的同时，直接将 working Tree 工作目录、 index 暂存区及 repository 都重置成目标 Reset 节点的內容,所以效果看起来等同于清空暂存区和工作区。

#### git reseet --mixed 或者说不加参数

保留工作目录，并清空暂存区
工作目录的内容和 --soft 一样会被保留，但和 --soft 的区别在于，它会把暂存区清空,并把原节点和 reset 节点的差异的文件放在工作目录，总而言之就是，工作目录的修改、暂存区的内容以及由 reset 所导致的新的文件差异，都会被放进工作目录

#### git reset --soft

保留工作目录，并把重置 HEAD 所带来的新的差异放进暂存区
--hard 会清空工作目录和暂存区的改动,而 --soft 则会保留工作目录的内容，并把因为保留工作目录内容所带来的新的文件差异放进暂存区。

### git cherry-pick

某次提交可以单独合并某次提交的代码，比如 A 分支有 3 次提交，想要把第 2 次合并到 B 分支。

如果遇到了代码冲突，解决冲突然后
git add .
git cherry-pick --continue

**--abort**
代码冲突，取消合并代码的事件

**--quit**
代码冲突，推出 cherry-pick，但是不会倒操作前的代码

### git fetch

差不多可以这样理解
git pull = git fetch + git merge
最常用的是，多人协同开发，别人新建的分支，在你 git branch -a 看不到的时候
执行一下 git fetch
完事

### git tag

通常发布的时候，每个版本都会打对应的 tag，方便后期回溯
git tag -a v2.4.9 （tag 的版本号）-m “描述”
-a 参数来创建一个带备注的 tag，备注信息由-m 指定。如果你未传入-m 则创建过程系统会自动为你打开编辑器让你填写备注信息。
git show 命令可以查看 tag 的详细信息，包括 commit 号等。