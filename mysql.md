安装MySQL在Linux

（1）查看自己是否安装了MySQL数据库



\[root@localhost /\]\# rpm -qa \| grep mysql



得到的结果如下：







这样说明已经安装了数据库，我们可以先对它进行卸载。。。



（2）卸载过程



卸载有两种方式，一种是普通删除，另一种是强力删除，当MySQL数据库有其它的依赖文件时，也进行删除。



分别是：rpm -e mysql 和rpm -e --nodeps mysql



（3）安装过程



首先，我们通过命令：yum list \| grep mysql来查看yum上提供的数据库可下载版本。







我们选择安装 mysql.i686，mysql-devel.i686，mysql-server.i686就行了。使用命令：



yum -y install mysql mysql-server mysql-devel



就可以安装好MySQL数据库了。。。



（4）数据库的相关配置



安装完MySQL数据库后，会发现多出了一个mysqld服务，这就是我们的数据库服务，启动它就是启动数据库。



启动方式：service mysqld start







我们可以使用命令：chkconfig --list \| grep mysqld来查看是否开机自动启动。如果2~5的都是on



说明是开机自动启动，否则如果不是。我们可以通过命令chkconfig mysqld on来设置成开机自动启动。







嗯，到了这里，我们就应该启动数据库设置密码了。



（5）数据库密码设置



先启动mysqld服务，即：service mysqld start，然后执行命令



mysqladmin -u root -p password 'root'

如何创建账号和分配权限

