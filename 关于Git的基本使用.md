@[TOC](目录)

### 时光穿梭机

## 1.创建仓库

什么是版本库呢？版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

1.所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

```
$ mkdir Git
$ cd Git
$ pwd
F:\Git
```

`pwd`命令用于显示当前目录。

2.第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：

```
$ git init
Reinitialized existing Git repository in F:/Git/.git/
```

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），我之前创建过，所以不是空仓库。同时可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

```
$ ls -ah
./  ../  .git/  code.TXT  Git/  keymap-win-mac.m
```

现在在目录底下修改文件read.txt

```
只争朝夕，不负韶华！
Git is a version control system.
```

第一步，用命令`git add`告诉Git，把文件添加到仓库：

```
$ git add read.txt
 git add keymap-win-mac.md
```

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```
$ git commit -m "1"
[master e5b5712] 1
 2 files changed, 151 insertions(+)
 create mode 100644 keymap-win-mac.md
 create mode 100644 read.TXT
```

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

`git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`2 insertions`：插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要`add`，`commit`一共两步呢？因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件，比如：

```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

## 2.版本回退

现在，你已经学会了修改文件，然后把修改提交到Git版本库，现在，再练习一次，修改readme.txt文件如下：

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
```

然后尝试提交：

```
$ git add read.txt
$ git commit -m "2"
[master 1094adb]2
 1 file changed, 2 insertion(+), 1 deletion(-)
```

像这样，你不断对文件进行修改，然后不断提交修改到版本库里

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
```



```
$ git add read.txt
$ git commit -m "3"
[master 1094adb]  3
 1 file changed, 2 insertion(+), 1 deletion(-)
```

现在，我们回顾一下`readme.txt`文件一共有几个版本被提交到Git仓库里了：

版本1：

```
只争朝夕，不负韶华！
Git is a version control system.
```

版本2：

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
```

版本3：

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
```

当然了，在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用`git log`命令查看：

```
$ git log
commit a2092c90784cd785d9996e4c705d61eb90707c36 (HEAD -> master)
Author: ITmxs <17752170152@163.com>
Date:   Fri Jun 19 11:14:18 2020 +0800

    3

commit 747bea05d65eb06f4f4f404a5511278b0f988ee3
Author: ITmxs <17752170152@163.com>
Date:   Fri Jun 19 11:12:04 2020 +0800

    2

commit e5b57127fa94fe81d36dafcab59d68db58720086
Author: ITmxs <17752170152@163.com>
Date:   Fri Jun 19 11:05:24 2020 +0800

    1

commit 021749f03ca0a1bfe5816e92f1d6e3aad757a78d
Author: ITmxs <17752170152@163.com>
Date:   Mon Jun 15 09:43:20 2020 +0800

    mxs
```

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：

```
$ git log --pretty=oneline
a2092c90784cd785d9996e4c705d61eb90707c36 (HEAD -> master) 3
747bea05d65eb06f4f4f404a5511278b0f988ee3 2
e5b57127fa94fe81d36dafcab59d68db58720086 1
021749f03ca0a1bfe5816e92f1d6e3aad757a78d mxs
34ec75333293a3c4661e1bb95d4b4379b79a5a96 zx
af878834f20b13225c878ced0255ae959aaaab5c (origin/master) zx
```

需要友情提示的是，你看到的一大串类似`1094adb...`的是`commit id`（版本号），和SVN不一样，Git的`commit id`不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的`commit id`和我的肯定不一样，以你自己的为准。为什么`commit id`需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：

好了，现在我们启动时光穿梭机，准备把`read.txt`回退到上一个版本，也就是`a`的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

现在，我们要把当前版本3`3`add distributed`，就可以使用`git reset`命令：

```
$ git reset --hard HEAD^
HEAD is now at 747bea0 2
```

看看`readme.txt`的内容是不是版本2

```
$ cat read.TXT
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
```

果然被还原了。

还可以继续回退到上一个版本不过且慢，然我们用`git log`再看看现在版本库的状态：

```
$ git log
commit 747bea05d65eb06f4f4f404a5511278b0f988ee3 (HEAD -> master)
Author: ITmxs <17752170152@163.com>
Date:   Fri Jun 19 11:12:04 2020 +0800

    2

commit e5b57127fa94fe81d36dafcab59d68db58720086
Author: ITmxs <17752170152@163.com>
Date:   Fri Jun 19 11:05:24 2020 +0800

    1

commit 021749f03ca0a1bfe5816e92f1d6e3aad757a78d
Author: ITmxs <17752170152@163.com>
Date:   Mon Jun 15 09:43:20 2020 +0800

    mxs

commit 34ec75333293a3c4661e1bb95d4b4379b79a5a96
Author: ITmxs <17752170152@163.com>
Date:   Mon Jun 15 09:35:43 2020 +0800

    zx

```

最新的那个版本已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个`3`的`commit id`是`a2092...`，于是就可以指定回到未来的某个版本：

```
$ git  reset --hard a2092
HEAD is now at a2092c9 3

```

```
$ cat read.txt
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
```

果然，我胡汉三又回来了。

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的`HEAD`指针，当你回退版本的时候，Git仅仅是把HEAD从指向3

```ascii
┌────┐
│HEAD│
└────┘
   │
   └──> ○ append3
        │
        ○ add 2
        │
        ○ 1
```

改为指向`2`：

```ascii
┌────┐
│HEAD│
└────┘
   │
   │    ○ append 3
   │    │
   └──> ○ add 2
        │
        ○ 1
```

然后顺便把工作区的文件更新了。所以你让`HEAD`指向哪个版本号，你就把当前版本定位在哪。

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？

在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`1`版本时，再想恢复到`3`，就必须找到`3`的commit id。Git提供了一个命令`git reflog`用来记录你的每一次命令：

```
$ git reflog
a2092c9 (HEAD -> master) HEAD@{0}: reset: moving to a2092
747bea0 HEAD@{1}: reset: moving to HEAD^
a2092c9 (HEAD -> master) HEAD@{2}: commit: 3
747bea0 HEAD@{3}: commit: 2
e5b5712 HEAD@{4}: commit: 1
021749f HEAD@{5}: reset: moving to 021749f
34ec753 HEAD@{6}: reset: moving to HEAD^
021749f HEAD@{7}: commit: mxs
34ec753 HEAD@{8}: commit: zx
af87883 (origin/master) HEAD@{9}: commit (initial): zx


```

## 3.工作区和暂存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

先来看名词解释。

### 3.1工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的GIT文件夹就是一个工作区：

![工作区](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200619114410693.png)



#### 3.1.1版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
zx
```

然后，在工作区新增一个`Love`文本文件（内容随便写）。

先用`git status`查看一下状态：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   read.TXT

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Git/
        love.TXT

no changes added to commit (use "git add" and/or "git commit -a")
```

Git非常清楚地告诉我们，`read.txt`被修改了，而`Love`还从来没有被添加过，所以它的状态是`Untracked`。

现在，使用两次命令`git add`，把`read.txt`和`Love`都添加后，用`git status`再查看一下：

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   love.TXT

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   read.TXT

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Git/
```

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支

```
$ git commit -m "understand how stage works"
[master e0b6320] understand how stage works
 1 file changed, 1 insertion(+)
 create mode 100644 love.TXT
```

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```
$ git status
On branch master
nothing to commit, working tree clean
```

#### 3.2管理修改

现在，假定你已经完全掌握了暂存区的概念。下面，我们要讨论的就是，为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。

你会问，什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

为什么说Git管理的是修改，而不是文件呢？我们还是做实验。第一步，对read.txt做一个修改，比如加一行内容：

```
$ cat read.txt
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
zx
xjg
```

```
$ git add read.txt
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   reads.txt
#
```

然后，再修改read.txt：

```
$ cat readme.txt 
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
```

提交：

```
$ git commit -m "git tracks changes"
[master 519219b] git tracks changes
 1 file changed, 1 insertion(+)
```

提交后，再看看状态：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

咦，怎么第二次的修改没有被提交？

别激动，我们回顾一下操作过程：

第一次修改 -> `git add` -> 第二次修改 -> `git commit`

你看，我们前面讲了，Git管理的是修改，当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用`git diff HEAD -- read.txt`命令可以查看工作区和版本库里面最新版本的区别：

```
$ git diff HEAD -- read.TXT
diff --git a/read.TXT b/read.TXT
index 2b0872f..5ecd938 100644
--- a/read.TXT
+++ b/read.TXT
@@ -4,3 +4,4 @@ Git is a version control system.
 我是MXS
 zx
 xjg
+绝处逢生，
```

可见，第二次修改确实没有被提交。

那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

好，现在，把第二次修改提交了，然后开始小结。

#### 3.3撤销修改

自然，你是不会犯错的。不过现在是凌晨两点，你正在赶一份工作报告，你在`read.txt`中添加了一行：

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
zx
xjg
绝处逢生，
我在玩游戏
```

在你准备提交前，一杯咖啡起了作用，你猛然发现了`我在玩游戏`可能会让你丢掉这个月的奖金！

既然错误发现得很及时，就可以很容易地纠正它。你可以删掉最后一行，手动把文件恢复到上一个版本的状态。如果用`git status`查看一下：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   read.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

你可以发现，Git会告诉你，`git checkout -- file`可以丢弃工作区的修改：

```
$ git checkout -- read.txt
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

现在，看看`readme.txt`的文件内容：

```
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
```

文件内容果然复原了。

`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

现在假定是凌晨3点，你不但写了一些胡话，还`git add`到暂存区了：

```
只争朝夕，不负韶华！
Git is a version control system.
世上无难事，只怕有心人
我是MXS
zx
xjg
绝处逢生，
boss是猪
$ git add read.txt
```

庆幸的是，在`commit`之前，你发现了这个问题。用`git status`查看一下，修改只是添加到了暂存区，还没有提交：

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   readme.txt
```

Git同样告诉我们，用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

```
$ git reset HEAD read.txt
Unstaged changes after reset:
M	readme.txt
```

`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

再用`git status`查看一下，现在暂存区是干净的，工作区有修改：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   read.txt
```

还记得如何丢弃工作区的修改吗？

```
$ git checkout -- read.txt
$ git status
On branch master
nothing to commit, working tree clean
```

整个世界终于清静了！

#### 3.4删除文件

在Git中，删除也是一个修改操作，我们实战一下，先添加一个新文件`test.txt`到Git并且提交：

```
$ git add love.txt

$ git commit -m "add test.txt"
[master b84166e] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了：

```
$ rm test.txt
```

这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，`git status`命令会立刻告诉你哪些文件被删除了：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    love.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：

```
$ git rm test.txt
rm 'test.txt'

$ git commit -m "remove love.txt"
[master d46f35e] remove love.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 love.txt
```

现在，文件就从版本库中被删除了。

 小提示：先手动删除文件，然后使用git rm <file>和git add<file>效果是一样的。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

```
$ git checkout -- love.txt
```

`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！