Centos7中安装JDK常见两种方式：在线安装openjdk和离线安装jdk-1.8.0

1. #### 在线安装OpenJDK

查看新系统是否安装java环境

```
[root@iZ4zeaehxxqhrn553tblkkZ /]# yum list installed |grep java
```

1
如果什么都没有显示则表示没有安装java，则可以直接安装。如果显示java的版本等信息，则需要先卸载老版本的java环境

卸载JDK相关文件
卸载openjdk

```
[root@iZ4zeaehxxqhrn553tblkkZ /]# yum -y remove java-1.8.0-openjdk*
```

1
卸载tzdata-java

```
[root@iZ4zeaehxxqhrn553tblkkZ /]# yum -y remove tzdata-java.noarch  

```

1
在线查看java的安装包列表

```
[root@iZ4zeaehxxqhrn553tblkkZ /]# yum -y list java*
```

1
安装选择的java版本ram包
[root@iZ4zeaehxxqhrn553tblkkZ /]# yum -y install java-1.8.0-openjdk
1
安装完成，查看java信息
[root@iZ4zeaehxxqhrn553tblkkZ /]#  java -version
1
到此在线安装完成。

1. #### 离线安装JDK

查看新系统是否安装java环境
[root@iZ4zeaehxxqhrn553tblkkZ /]# yum list installed |grep java
1
如果什么都没有显示则表示没有安装java，则可以直接安装。如果显示java的版本等信息，则需要先卸载老版本的java环境

卸载JDK
[root@iZ4zeaehxxqhrn553tblkkZ /]# rpm -e –nodeps
1
安装jdk1.8
首先创建一个java的文件夹
[root@iZ4zeaehxxqhrn553tblkkZ /]# mkdir /home/work/java
1
上传jdk-8u144-linux-x64.tar.gz
将本地下载的jdk上传到 /home/work/java 目录下

[root@iZ4zeaehxxqhrn553tblkkZ /]# cd /home/work/java
[root@iZ4zeaehxxqhrn553tblkkZ /]# rz 
1
2
解压
[root@iZ4zeaehxxqhrn553tblkkZ /]# cd /home/work/java
[root@iZ4zeaehxxqhrn553tblkkZ /]# tar -zxvf jdk-8u144-linux-x64.tar.gz
1
2
配置环境变量
在/etc/profile文件的末尾加上以下配置:

[root@iZ4zeaehxxqhrn553tblkkZ /]# vim /etc/profile
1
末尾增加如下内容：

JAVA_HOME=/home/work/java/jdk1.8.0_144
JRE_HOME=/home/work/java/jdk1.8.0_144/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH
1
2
3
4
5
profile文件立即生效
[root@iZ4zeaehxxqhrn553tblkkZ /]# source /etc/profile
1
测试
[root@iZ4zeaehxxqhrn553tblkkZ /]# java -version
java version "1.8.0_144"
Java(TM) SE Runtime Environment (build 1.8.0_144-b01)
Java HotSpot(TM) 64-Bit Server VM (build 25.144-b01, mixed mode)
1
2
3
4
离线安装完成
————————————————
版权声明：本文为CSDN博主「bellus-」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/xiaoyu19910321/article/details/106291856



