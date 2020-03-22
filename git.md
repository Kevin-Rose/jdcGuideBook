#### **centos7下git的使用和配置

## **1.下载git，使用命令：

#### **

#### **1 yum install git

#### **2.配置git：

#### **

#### **1 git config --global user.name "Your Name"

#### **2 git config --global user.email "email@example.com"

#### **3 \#查看配置是否生效

#### **4 git config --list

#### **3.创建本地仓库：

#### **

#### **1 \#创建目录

#### **2 mkdir gitspace

#### **3 cd gitspace

#### **4 git init

#### **这时git本地仓库已经搭好了，测试一下：

#### **

#### **创建1个readme，执行git status ./

#### **

#### **

#### **

#### **git add该文件：

#### **

#### **1 \#git add .添加所有文件

#### **2 git add readme

#### **再使用git status查看：

#### **

#### **

#### **

#### **readme已经加入暂存区，但还没提交本地仓库

#### **

#### **再使用git commit提交：

#### **

#### **1 git commit -m "add readme"

#### **

#### **

#### ** 

#### **

#### ** 提交后查看，本地已经没有需要提交的记录。

#### **

#### **4.配置远程仓库：

#### **

#### **1）先在自己的linux服务器本地生成ssh key，使用命令 “ssh-keygen -t rsa -C "your\_email@youremail.com"”，your\_email是你的email，执行时一路按回车就行，这会在当前用户下生成1个公钥id\_rsa.pub和一个私钥id\_rsa,id\_rsa.pub后面配置git要用到。

#### **

#### ** 

#### **

#### **

#### **

#### **2\)在github上注册一个新用户，注册成功后，在settings设置ssh key：

#### **

#### **settings:

#### **

#### **

#### **

#### **设置ssh key：

#### **

#### **

#### **

#### **ssh key为前面服务器上的id\_rsa.pub，打开整个拷贝到key中：

#### **

#### **

#### **

#### **添加成功后，点击+号新增一个仓库：new repository**

#### 


