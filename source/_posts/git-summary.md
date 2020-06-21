---
title: Git常用工作流程
---
本文总结了我在工作中的一般git开发提交代码流程，以及一些比较好用的git命令
### 分支开发
    来了一个新需求，一般基于develop分支，checkout一个feature branch，完成开发后，checkout到develop分支，然后merge到develop分支。以前我一直在develop分支开发，弊端就是，每次别人有个新改动，我要立马使用的时候，需要先提交本地未完成的代码，导致无效的提交。这个时候就可以先checkout到develop分支，拉取代码，然后查看代码效果。feature和develop就不会冲突
```
$ git checkout developp
$ git checkout feature_branch
$ ## some code work in feature branch
$ git checkout develop
$ git merge feature_branch
```
### 代码提交
git add & commit 之后拉取远程分支代码，有两种方法
1.直接git pull, 会自动创建一个merge的提交记录，会污染提交历史(merge requset的无效提交记录)
2.git fetch origin develop 然后 git rebase origin/develop, 这种方法是更新本地develop分支基于的节点（rebase我的理解是换成远程分支上最新的提交节点，合并提交记录，不会产生冗余commit），如果有冲突，就按照提示，解决冲突然后git rebase –continue；或者放弃rebase： git rebase –abort
所以我一般用的是：
```
$ git fetch origin develop
$ git rebase origin/develop
```
### 回滚操作

  以前只知道git reset –hard commit_hash_code, 最近发现这个命令暗藏玄机, hard会把工作区包括staged的内容清空，回到指定的commit节点。但我有时候并不想丢弃本地未提交的代码，怎么办呢？把hard 换成soft试试
  ```
git reset --soft c56da67(git commit hase code)
  ```
  这个命令会把本地代码回退到指定commit节点，然后把工作区的内容与该提交节点的差异内容放入暂存区，也就是执行了git add；感觉发现了新大陆（浅薄无知的我）
  
### 代码暂存

  当需要中断当前分支，切换到其他分支，git会提示我们要提交，否则会丢失工作区内容，但我现在不想提交，这个时候就可以用
```
$ git stash //压栈
$ git stash list //栈记录
$ git stash clear // 清空
$ git stash apply // 恢复暂存代码
```
  