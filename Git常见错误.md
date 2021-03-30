





# 1.Unable to create 'F:/Git/.git/index.lock': File exists.

```
$ git add doc-public
fatal: Unable to create 'F:/Git/.git/index.lock': File exists.
解决办法：
执行
$ rm -f .git/index.lock
再提交
$ git add doc-public
```

# 2.committing is not possible because you have unmerged files.

Committing is not possible because you have unmerged files. 由于您没有合并的文件，因此无法提交。

解决方法
用git diff或者git status 查看哪些文件冲突，有冲突的会提示：
++<<<<<<< HEAD

++<<<<<<< new_branch

修改你的冲突的文件，然后用git add xxx，把你修改的文件全部都添加进去。之后就是正常的提交流程
关于Git推送error：failed to push some refs to 'git@gitee.com:name/project.git'



# 3.项目推送时遇Git推送错误：

error: failed to push some refs to ‘git@gitee.com:name/project.git’

1、分析：

这个问题的产生是因为远程仓库与本地仓库并不一致所造成。

2、解决方案：

那么我们把远程库同步到本地库就可以了。

执行命令：

```
git pull --rebeise origin master
```

将远程仓库中的更新合并到本地仓库，–rebase的作用是取消掉本地仓库中刚刚的commit

然而未果，出现错误：

```
error: src refspec master does not match any
```


分析：引起该错误的原因是，目录中没有文件，空目录不能提交。

依次执行：

```
git pull origin master
git push origin master
```


解决！

一般而言，正常的推送流程应为：

1、在github上创建项目

2、使用git clone https://github.com/name/project.git克隆到本地

3、编辑项目

4、git add . （将变更提交至缓存区）

5、git commit -am “提交说明（注释）”

6、git push origin master 将本地变更推送至远程仓库master分支

此时如果在github的remote上已经有了文件，会出现error。那么应当先pull一下，即：

```
git pull origin master
```


随即push即可。

```
git push origin master
```

# 4.完美解决 fatal: unable to access 'https://github.com/.../.git': Could not resolve host: github.com

只需要在命令行中执行

```
git config --global --unset http.proxy 
git config --global --unset https.proxy
```

# 5.git提交分支出现already up to date的问题和解决


今天提交分支的时候出现：already up to date的报错
通过查阅资料
输入以下命令得以解决：

git checkout master
git reset --hard 分知名
git push --force origin master

成功！！！

# 6.git提交分支出现already up to date的问题和解决


今天提交分支的时候出现：already up to date的报错
通过查阅资料
输入以下命令得以解决：

```
$ git branch   查看当前分支
git checkout master //切换主分支
git reset --hard 分知名
git push --force origin master
```

成功！！！

# 7.强制提交	

```
git add .
git commit -m "your comment"
git push -u origin master -f
```

