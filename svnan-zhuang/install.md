rpm -qa subversion



检验已经安装的SVN版本信息 

\[root@localhost modules\]\# svnserve --version

C:\WINDOWS\system32&gt;netstat -ano \| findstr 8080

  TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       27040

  TCP    \[::\]:8080              \[::\]:0                 LISTENING       27040



C:\WINDOWS\system32&gt;taskkill /F /PID 27040

成功: 已终止 PID 为 27040 的进程。



C:\WINDOWS\system32&gt;netstat -ano \| findstr 8080

  TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       24516

  TCP    \[::\]:8080              \[::\]:0                 LISTENING       24516

  TCP    \[::1\]:54784            \[::1\]:8080             TIME\_WAIT       0



C:\WINDOWS\system32&gt;netstat -ano \| findstr 8080



C:\WINDOWS\system32&gt;taskkill /F /PID 24516

错误: 没有找到进程 "24516"。

\#svn 

\[root@localhost password\]\# killall svnserve    //停止 

\[root@localhost password\]\# svnserve -d -r /opt/svn/repositories  // 启动 



C:\WINDOWS\system32&gt;netstat -ano \| findstr 8080



C:\WINDOWS\system32&gt;P



http://www.cnblogs.com/zhoulf/archive/2013/02/02/2889949.html



\[root@iZ2zedwxdhlj7s7ae9rmhmZ ~\]\# cd /usr/local/tomcat/bin

\[root@iZ2zedwxdhlj7s7ae9rmhmZ bin\]\#  ./startup.sh 



   46  ls /etc/my.cnf

   47  rpm -qa \| grep mysql

   48  rpm -qa \| grep mariadb

   49  mysql

   50  service mariadb start

   51  service mariadb status





netstat -ano \| findstr ":80 "

tasklist /fi "PID eq 4"

-------------------------------------------------------------------------------------

\#检查是否安装了低版本的SVN

\[root@localhost /\]\# rpm -qa subversion



\#卸载旧版本SVN

\[root@localhost modules\]\# yum remove subversion

