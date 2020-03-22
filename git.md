# [centos7下git的使用和配置](https://www.cnblogs.com/daniaofighter/p/9452661.html)

1.下载git，使用命令：

```
1
yum
install
 git
```

2.配置git：

```

```

3.创建本地仓库：

```
1
#创建目录

2
mkdir
 gitspace

3
cd gitspace

4
 git init
```

这时git本地仓库已经搭好了，测试一下：

创建1个readme，执行git status ./

![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180809235411786-853231287.png)

git add该文件：

```
1
#git add .添加所有文件

2
 git add readme
```

再使用git status查看：

![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180810000007458-1142850348.png)

readme已经加入暂存区，但还没提交本地仓库

再使用git commit提交：

```
1
 git commit -m 
"
add readme
"
```

![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180810000207106-1765843665.png)



 提交后查看，本地已经没有需要提交的记录。

4.配置远程仓库：

1）先在自己的linux服务器本地生成ssh key，使用命令 “ssh-keygen -t rsa -C "your\_email@youremail.com"”，your\_email是你的email，执行时一路按回车就行，这会在当前用户下生成1个公钥id\_rsa.pub和一个私钥id\_rsa,id\_rsa.pub后面配置git要用到。



![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180810001935557-215686148.png)

2\)在github上注册一个新用户，注册成功后，在settings设置ssh key：

settings:

![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180810002225015-1792098264.png)

设置ssh key：

![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180810002333035-601958171.png)

ssh key为前面服务器上的id\_rsa.pub，打开整个拷贝到key中：

![](https://images2018.cnblogs.com/blog/964574/201808/964574-20180810002646908-587736849.png)

添加成功后，点击+号新增一个仓库：new repository

