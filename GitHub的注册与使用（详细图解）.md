

@[TOC]()

[Git下载](https://pc.qq.com/detail/13/detail_22693.html)



# 一、gihub账号注册与仓库创建

## 1.注册

**地址: https://github.com/
输入账号、邮箱、密码,然后点击注册按钮.**

注册的时候最好取一个有意义的名字，比如姓名全拼，昵称全拼，如果被占用，可以加上有意义的数字.
本文中假设用户名为 ITmxs(我的博客名的全拼)

## 2. 初始设置

 

注册完成后,选择免费账号完成设置。

## 3.验证账号

 新建仓库

![img](https://img-blog.csdn.net/20160509142614145)

## 4.发现邮箱地址未验证，登录你注册时的邮箱，验证

![image-20200615074838697](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200615074838697.png)

## 5.新建仓库

 

输入仓库名，点击创建仓库，创建成功

![image-20200615075034157](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200615075034157.png)

## 



# 二，本地仓库上传到github仓库

## 1.我在F盘下创建了Git目录

![image-20200614203957047](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614203957047.png)

## 2.鼠标右击打开

![image-20200614204133596](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614204133596.png)

## 3.输入

```
 git add code.TXT
```

## 4.发现报错

```
fatal: not a git repository (or any of the parent directories): .git
```

## 5.解决办法

输入

```
git init
```

重新输入即可创建成功

## 6.配置用户名和邮箱



![image-20200614204757431](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614204757431.png)

## 7.提交成功

![image-20200614205601551](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614205601551.png)



找不到ssh-keygen命令是因为你的工作目录不在ssh-keygen.exe所在目录下，导致找不到命令，所以切换工作目录到ssh-kengen所在目录(Git/usr/bin/)即可。以我为例，我的Git安装在D盘Git下，所以进行操作 cd D:/Git/usr/bin/ ，然后执行 ssh-keygen -t rsa -C “您的邮箱地址” 即可

![image-20200614212406139](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614212406139.png)

![image-20200614212327832](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614212327832.png)



## 8、生成SSH密钥



$ ssh-keygen -t rsa -C "17752170152@163.com"
按3个回车，密码为空。

![image-20200614212022260](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614212022260.png)

## 9.输入之后出现以上情况，然后在输入git push origin master 之后会出现一个

![image-20200614213538320](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614213538320.png)

![img](https://img-blog.csdn.net/20170912224136180?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSGFuYW5pX0ppYQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## 10.在C:\Users\luckly\.ssh目录下找到id_rsa.pub复制里面所有内容

![image-20200614212725871](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614212725871.png)







## 11.登录你的gihub账号，点击Your profile



![img](https://img-blog.csdn.net/20160509150204773)

## 12然后点击Edit profile





![img](https://img-blog.csdn.net/20160509150433524)



## 13选择SSH并新建一个SSH Key

![img](https://img-blog.csdn.net/20160509151206355)

![image-20200614213111283](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614213111283.png)







其中Title中的名称可以任意填写，将C:\Users\luckly\.ssh目录下id_rsa.pub复制的所有内容粘贴到Key中，点击Add SSH Key，SSH密钥完成





## 14、 添加新的远程仓库



 **添加新的远程仓库**

$ git remote add origin git@github.com/ITmxs/mygit.git其中红色部分的URL时是gihub中的SSH

远程提交完成！！！！！

![image-20200614213538320](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614213538320.png)

## 15.如果之后出现这种情况的话，就是登陆失败了，这时候你就需要输入你GitHub的账号名称

![img](https://img-blog.csdn.net/20170912224220863?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSGFuYW5pX0ppYQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



## 16.远程提交

![image-20200614211926084](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614211926084.png)



## 17。现在打开你的GitHub网站，找到你创建的库，发现今天的格子已经绿了，说明你已经上传了你刚刚所创建的文件。

![image-20200614214040960](https://mxszs.oss-cn-beijing.aliyuncs.com/img/image-20200614214040960.png)

远程提交完成！！！！！