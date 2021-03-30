#### 标签管理

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

Git有commit，为什么还要引入tag？

“请把上周一的那个版本打包发布，commit号是6a5819e...”

“一串乱七八糟的数字不好找！”

如果换一个办法：

“请把上周一的那个版本打包发布，版本号是v1.2”

“好的，按照tag v1.2查找commit就行！”

所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

#### 创建标签

在Git中打标签非常简单，首先，切换到需要打标签的分支上：

```
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
```

然后，敲命令`git tag <name>`就可以打一个新标签：

```
$ git tag v1.0
```

可以用命令`git tag`查看所有标签：

```
$ git tag
v1.0
```

默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了：

```
$ git log --pretty=oneline --abbrev-commit
aed0d20 (HEAD -> master, tag: v1.0, origin/master) bug fix 01
6ab5982 (issue-101) bug 01
007b7aa merge with no-ff
a66f3d4 (origin/dev, dev) add 004
99fa0a0 ccc
aa309c8 fff
5174635 8zx
06e428d remove love.TXT
284196c git track
e0b6320 understand how stage works
a2092c9 3
747bea0 2
e5b5712 1
021749f mxs
34ec753 zx
af87883 zx

```

比方说要对`mxs`这次提交打标签，它对应的commit id是`021749f`，敲入命令：

```
$ git tag v0.1 021749f
```

再用命令`git tag`查看标签：

```
$ git tag
v0.9
v1.0
```

注意，标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息：

```
$ git show v0.1
commit 021749f03ca0a1bfe5816e92f1d6e3aad757a78d (tag: v0.1)
Author: ITmxs <17752170152@163.com>
Date:   Mon Jun 15 09:43:20 2020 +0800

    mxs

diff --git a/code.TXT b/code.TXT
index fdd8d4f..f8e2332 100644
--- a/code.TXT
+++ b/code.TXT
@@ -1 +1,2 @@
-ITmxs
\ No newline at end of file
+ITmxs
+<C4>Ǻð<C9>
\ No newline at end of file


```

可以看到，`v0.1`确实打在`mxs`这次提交上。

还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：

```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

用命令`git show <tagname>`可以看到说明文字：

```
$ git show v0.1
tag v0.1
Tagger: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 22:48:43 2018 +0800

version 0.1 released

commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (tag: v0.1)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

diff --git a/readme.txt b/readme.txt
...
```

 注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

#### 操作标签

如果标签打错了，也可以删除：

```
$ git tag -d v0.1
Deleted tag 'v0.1' (was 021749f)
```

因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令`git push origin <tagname>`：

```
$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
 * [new tag]         v1.0 -> v1.0
```

或者，一次性推送全部尚未推送到远程的本地标签：

```
$ git push origin --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
 * [new tag]         v0.9 -> v0.9
```

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：

```
$ git tag -d v1.0
Deleted tag 'v1.0' (was aed0d20)

```

然后，从远程删除。删除命令也是push，但是格式如下：

```
$ git push origin :refs/tags/v1.0
To https://github.com/ITmxs/mygit.git
 - [deleted]         v1.0


```

要看看是否真的从远程库删除了标签，可以登陆GitHub查看。