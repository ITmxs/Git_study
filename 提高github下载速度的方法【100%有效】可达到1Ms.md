@[TOC](目录)

最近在Github找项目，然后 拉取到本地进行学习，但是发现国内从github上面下载代码的速度峰值通常都是20kB/s。这种速度对于那些小项目还好，但是对于大一些的并且带有很多子模块的项目来讲就有点耽误时间了。

在这儿我也是学习了别人的经验之后，总结出了自己的方法 ，下载速度可以达到 1~2MB/s，接下来我就会对 这个方法做一剧透：

# 一，方法一

## 1.利用开源中国提供的代码仓库（gitee）

我想对于经常使用git的人来讲，很可能已经知道了。对于新手刚接触git的人来讲，可能你只知道github。对于gitee了解不多

这儿给出[Gitee官网连接](https://gitee.com/)

开源中国提供的代码仓库提供了一个功能，就是它可以将github账号中的代码 clone 到开源中国的账户中去。这个代码仓库叫做 码云 ，没错就是码云?。
要求你有一个github账户，一个码云gitee账户。

## 2.将github上面你想要搞下来的项目首先 frok 到你自己的github的账户中去。

耗时:一瞬间

登录gitee[Gitee官网连接](https://gitee.com/)，没有的自行注册。网页中有添加项目的按钮，一个加号。点击加号，下拉列表里面有 迁移github项目 的选项

点开后按照提示关联自己的github账号，之后选择你要迁移的项目，按提示操作。耗时:不到三分钟。

按照 clone  github项目方法， clone 迁移到gitee账户中的项目。区别是 clone 链接换成了目标项目在gitee中的链接。通常下载速度是以

MB/s为单位的。

按照上面的方法，基本上不再需要整夜挂机 clone 代码了。

最近重新看了下，其实上面的步骤有些繁琐，其可以更简单，新建仓库直接设置远程仓库地址。

# 二，方法二

## 1.第一步新建仓库：

<img src="https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200621121623073.png" alt="新建仓库" style="zoom:50%;" />

## 2.第二步：

以github仓库https://github.com/norybaby/poet.git举例

选择导入已有仓库

<img src="https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200621122146938.png" alt="image-20200621122146938" style="zoom:67%;" />

## 3.第三步：

![image-20200621123230669](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200621123230669.png)

## 4.第四步

![image-20200621122957977](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200621122957977.png)

# 三，提高下载子模块的速度

有的项目里用到了第三方代码仓库，但是在你使用 clone 指令的时候这些子模块 submodule 并不会自动下载，因为他们在另外的地址中

存放。你需要 clone 完目标项目后，执行

git submodule update --init --recursive

才会将目标项目所需要的依赖子模块下载下来。github项目中所用到的子模块依然是放在了github上。这就很悲剧了，这意味着你在执行

上面指令后，依然需要面对上面的20KB/s的速度。虽然此时并不会显示出来，然而等待依然很久

我们同样使用上面加速 clone 的思路。

从下载的项目中找到其使用的 submodule 的链接是哪里。

打开上一步中的链接，将使用的目标子模块的代码同样 frok 到自己的github账户中，之后同样的方法迁移到gitee中去。有多个子模块就

多重复几次操作，同样的套路。

将原项目使用的 submodule 模块的链接地址修改为子模块迁移到gitee中后的地址。

这时再去执行git submodule update --init --recursive 。

以上就是提高下载子模块速度的思路。具体每步的操作，请自行搜索，网上一搜一大片。
附：：
关于如何修改submodule连接地址看下面

# git submodule的使用

开发过程中，经常会有一些通用的部分希望抽取出来做成一个公共库来提供给别的工程来使用，而公共代码库的版本管理是个麻烦的事情。今天无意中发现了git的git submodule命令，之前的问题迎刃而解了。

### 添加

为当前工程添加submodule，命令如下：

```
git submodule add 仓库地址 路径
```

其中，仓库地址是指子模块仓库地址，路径指将子模块放置在当前工程下的路径。 
注意：路径不能以 / 结尾（会造成修改不生效）、不能是现有工程已有的目录（不能順利 Clone）

命令执行完成，会在当前工程根路径下生成一个名为“.gitmodules”的文件，其中记录了子模块的信息。添加完成以后，再将子模块所在的文件夹添加到工程中即可。

### 删除

submodule的删除稍微麻烦点：首先，要在“.gitmodules”文件中删除相应配置信息。然后，执行“git rm –cached ”命令将子模块所在的文件从git中删除。

### 下载的工程带有submodule

当使用git clone下来的工程中带有submodule时，初始的时候，submodule的内容并不会自动下载下来的，此时，只需执行如下命令：

```
git submodule update --init --recursive
```

即可将子模块内容下载下来后工程才不会缺少相应的文件。

git是我们每天都会使用的工具，但是一般的使用还是直接通过几个简单的命令，例如:

```csharp
git add .
git commit -m "..."
git push origin master
```

对于上面简单的步骤，我们每天都会重复无数次，所以巨懒如我就干脆搞个小脚本，直接点一下就提交了。。

# Window使用bat脚本一键提交代码

直接新建文件，保存成.bat格式，编辑如下：

```bash
title GIT提交批处理——萌小肆专用
color 16


echo 开始提交代码到本地仓库
echo 当前目录是：%cd%

echo 开始添加变更
echo ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
git add -A .
echo 执行结束！
echo ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

echo;
echo 提交变更到本地仓库
echo ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
set /p declation=输入修改:
git commit -m "%declation%"
echo ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

echo;
echo 将变更情况提交到远程git服务器
echo ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
git push origin master
echo ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

echo;
echo 批处理执行完毕！
echo;

pause
```


