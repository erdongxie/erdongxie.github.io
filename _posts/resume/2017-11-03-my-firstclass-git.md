---
layout: post
title: Git入门
category: resume
description: 能时光穿梭的Git
---
## 我们都有版本管理的需要


-论文需要修改，想删除一个段落，但是又怕找不回来，这是有办法的，先把当前文件"另存为..."生成一个新的文件，然后再接着改，改到一定程度再"另存为..."，生成另一个新文件，于是你有了以下的奇观。
![original-version-control](https://raw.githubusercontent.com/xneo123/xneo123.github.io/master/images/class/git/%E5%8E%9F%E5%A7%8B%E7%9A%84%E6%89%8B%E5%8A%A8%E7%89%88%E6%9C%AC%E8%AE%B0%E5%BD%95.png)
过了一段时间，你想找回那个你特别喜欢的段落，但是实在是记不住是哪个文件里面的了，这时你只有一个个的打开这些文件，挨个寻觅，太麻烦了~~。

### 但是下一种场景才是要要了你的小命

-遇到跟同学一起合作的课程设计，你是这个课程设计的负责人，有三个同学跟你一起来完成：小芳，小明，小胖。课程设计项目A正式开始，你设计了一个文档，大家把各自分工要写的东西按照一定的格式放在你的模板里面。小红把她整理的数据贴在了模板里面，然后用u盘（也可以是E-mail)拷给了你。你继续着你的数据收集和整理。一天后，小明你和小胖一人发了一份他们整理好的数据给你，然后你现在需要做的事情多了起来，需要挨个把他们的数据与你的数据和小红的数据进行合并（merge)并且要做一个文档记录。突然你发现，小红并不是跟你一起做课程设计的同学，小芳才是，而小芳压根忘记了这个课程设计（权限管理）。我的天啊~~
你在想如果有一个这样的东西，或许就没有这么人艰不拆了。
![original-version-control](https://raw.githubusercontent.com/xneo123/xneo123.github.io/master/images/class/git/original-manual-doc-log.png)
这样你就结束了手动管理多个版本的"史前"时代。进入了版本控制的20世纪。

## Git的前世今生

-SVN和CVS

-集中式和分布式

-万恶的bitKeeper

-Git到底该怎么读？

### 安装git

-在Linux上安装Git

-在Mac上安装Git

-在windows上安装Git

### 课堂实践1
在自己的电脑上安装好Git，并获得以下的截图
![original-version-control](https://raw.githubusercontent.com/xneo123/xneo123.github.io/master/images/class/git/git-install-successfully.png)

### 创建你的第一个版本库

#### 第一步：在一个合适的位置创建你的Git仓库（repository)。

ps：如何在Windows上，有linux的感觉~

![git-bash](https://raw.githubusercontent.com/xneo123/xneo123.github.io/master/images/class/git/enter-git-bash.gif)

#### 第二步：通过git init命令把这个目录变成Git可以管理的仓库。

```shell
$ git init
Initialized empty Git repository in C:/git/learngit/.git/
```
创建一个readme.txt文件：
文件内容为：

<pre>
Git is a version control system.
Git is free software.
</pre>

#### 第三步：把你的文件添加(add)到仓库
```shell
$ git add readme.txt
```
#### 第四步：把你的文件提交(commit)到仓库
```shell
$ git commit -m "write a readme file"
[master (root-commit) 5022828] write a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```
#### HINT
```shell
$ git add *
```
可以添加当前目录及子目录所有的文件
```shell
$ git commit
```
可以一次提交很多文件

### 我有一台时光机

#### 第一步修改文件readme.txt为：
<pre>
Git is a distributed version control system.
Git is free software.
</pre>

运行git status查看结果
```shell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

git status命令可以让我们时刻掌握仓库当前的状态，上⾯的命令告诉我们，readme.txt被
修改过了，但还没有准备提交的修改。

虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，⾃然是很好
的。⽐如你放了个寒假，第⼀天回到学校，已经记不清上次怎么修改的
readme.txt，所以，需要⽤git diff这个命令看看：
```shell
$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.
```
####HINT
git status:随时掌握工作区状态
git diff:可以查看修改内容


#### 第二步提交
```shell
$ git add *
warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.

neoan@NeoWorkLapTop MINGW64 /c/git/learngit (master)
$ git commit -m "add distributed"
[master b8b8df2] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
```

#### 第三步 版本回退
先回顾下我们有哪两个版本了
<pre>
版本1：write a readme file
Git is a version control system.
Git is free software.
版本2：add distributed
Git is a distributed version control system.
Git is free software.
</pre>

在实际⼯作中，我们脑⼦⾥怎么可能记得⼀个⼏千⾏的⽂件每次都改了什么内容，
不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在Git
中，我们⽤git log命令查看：

```shell
$ git log
commit b8b8df2378e7e377ed654e1e3d25493d3713affc
Author: Neo Xie <neoanderson1987@126.com>
Date:   Sat Nov 4 08:56:30 2017 +0800

    add distributed

commit 502282806e2e022f561990207cd6b369bfcff503
Author: Neo Xie <neoanderson1987@126.com>
Date:   Sat Nov 4 01:16:08 2017 +0800

    write a readme file
```

 如果嫌输出信息太多，看得眼花缭乱的，可以试试加上
--pretty=oneline参数：
```shell
$ git log --pretty=oneline
b8b8df2378e7e377ed654e1e3d25493d3713affc add distributed
502282806e2e022f561990207cd6b369bfcff503 write a readme file
```
你看到的⼀⼤串类似“b8b8df....13affc”的是commit id（版本
号），和SVN不⼀样，Git的commit id不是1，2，3……递增的数字，⽽是⼀个SHA1计算
出来的⼀个⾮常⼤的数字，⽤⼗六进制表⽰，⽽且你看到的commit id和我的肯定不⼀样，
以你⾃⼰的为准。为什么commit id需要⽤这么⼀⼤串数字表⽰呢？因为Git是分布式的版
本控制系统，后⾯我们还要研究多⼈在同⼀个版本库⾥⼯作，如果⼤家都⽤1，2，3……作
为版本号，那肯定就冲突了。

我们想把readme.txt回退到write a readme file这个版本怎么做呢？

```shell
$ git reset --hard HEAD^
HEAD is now at 5022828 write a readme file

$ cat readme.txt
Git is a version control system.
Git is free software.
$ git log
commit 502282806e2e022f561990207cd6b369bfcff503
Author: Neo Xie <neoanderson1987@126.com>
Date:   Sat Nov 4 01:16:08 2017 +0800

    write a readme file
```
现在版本已经回退到write a readme file这个版本了

我怎么又到add distributed这个版本呢？

只要上⾯的命令⾏窗⼝还没有被关掉，你就可以顺着往上找啊找啊，找
到那个“add distributed”的commit id是“b8b8df...”，于是就可以指定回到未来的某个
版本：

```shell
$ git reset --hard b8b8df
HEAD is now at b8b8df2 add distributed
$ cat readme.txt
Git is a distributed version control system.
Git is free software.
$ git log
commit b8b8df2378e7e377ed654e1e3d25493d3713affc
Author: Neo Xie <neoanderson1987@126.com>
Date:   Sat Nov 4 08:56:30 2017 +0800

    add distributed

commit 502282806e2e022f561990207cd6b369bfcff503
Author: Neo Xie <neoanderson1987@126.com>
Date:   Sat Nov 4 01:16:08 2017 +0800

    write a readme file
```
此时我们又回到了add distributed这个版本。

如果我不小心关掉了命令行窗口，或者手残输入了clear是不是我就回不去未来了呢？答案是否定的。
git 怎么能允许如此的事情发生，可以使用git reflog命令查看：
```shell
$ git reflog
b8b8df2 HEAD@{0}: reset: moving to b8b8df
5022828 HEAD@{1}: reset: moving to HEAD^
b8b8df2 HEAD@{2}: commit: add distributed
5022828 HEAD@{3}: commit (initial): write a readme file
```

#### HINT

-HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使⽤命
令git reset --hard commit_id。
 
-穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

-要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。


## 课堂大作业：
1、编写一个文本文件，形成三个版本
<pre>
版本1： write a homework.txt
I'm a student.
版本2： add Fifth Tec
I'm a Fifth Tec student.
版本3：add CTO
I'm a Fifth Tec CTO's student.
</pre>
在这三个版本中随心所欲的切换。

可能会用到的命令:
<pre>
git init:初始化一个git版本库
git status:查看当前工作区状态
git add:添加文件
git commit:提交文件
git log:查看日志
git reflog:查看命令历史
git reset --hard <commit id>:切换版本
git reset --hard HEAD^:回退到上一个版本
</pre>

## 本课小结：
<pre>
1、版本管理是21世纪不得不学习的事务，如同你的驾照。
2、git的由来是Linus大神继linux之后给世界的一大宝物。
3、git常用命令
    创建你的版本库---git init
    添加文件---git add
    提交文件---git commit
    查看工作区状态---git status
    日志---git log
    命令历史---git reflog。
    切换到任意一个版本---git reset --hard <commit id>
</pre>
