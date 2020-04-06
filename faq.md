1. ### 经常运行过程中出现 Liquibase - Waiting for changelog lock

Waiting for changelog lock....

Running the migration script for a database may produce this:

...INFO … Liquibase: Waiting for changelog lock....

解决方法： 看下那个机器锁住了database，执行下面语句；

USE \[Database Name\]

SELECT \* FROM DATABASECHANGELOGLOCK;

一般情况下是本机锁住的；则通过下面sql解锁

UPDATE DATABASECHANGELOGLOCK

SET locked=0, lockgranted=null, lockedby=null

WHERE id=1

###### LiquiBase实战总结[https://blog.csdn.net/Netbug\_NB/article/details/40075493?depth\_1-utm\_source=distribute.pc\_relevant.none-task-blog-BlogCommendFromBaidu-10&utm\_source=distribute.pc\_relevant.none-task-blog-BlogCommendFromBaidu-10](https://blog.csdn.net/Netbug_NB/article/details/40075493?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-10&utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-10)



