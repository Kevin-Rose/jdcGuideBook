\#打开终端

cd /usr/local/tomcat/bin



./usr/local/tomcat/bin/shutdown.sh & ./usr/local/tomcat/bin/startup.sh

\#执行

bin/startup.sh \#启动tomcat

bin/shutdown.sh \#停止tomcat

tail -f logs/catalina.out \#看tomcat的控制台输出；

\#看是否已经有tomcat在运行了

ps -ef \|grep tomcat 

\#如果有，用kill;

kill -9 pid \#pid 为相应的进程号

例如 ps -ef \|grep tomcat 输出如下

sun 5144 1 0 10:21 pts/1 00:00:06 /java/jdk/bin/java -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djava.endorsed.dirs=/java/tomcat/common/endorsed -classpath :/java/tomcat/bin/bootstrap.jar:/java/tomcat/bin/commons-logging-api.jar -Dcatalina.base=/java/tomcat -Dcatalina.home=/java/tomcat -Djava.io.tmpdir=/java/tomcat/temp org.apache.catalina.startup.Bootstrap start

则 5144 就为进程号 pid = 5144

kill -9 5144 就可以彻底杀死tomcat

\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#3

http://www.cnblogs.com/jaylon/p/4905769.html

