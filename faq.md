经常运行过程中出现

Liquibase - Waiting for changelog lock

Waiting for changelog lock....

Running the migration script for a database may produce this:

...INFO … Liquibase: Waiting for changelog lock....

解决方法： 看下那个机器锁住了database，执行下面语句；

USE \[Database Name\]

SELECT \* FROM DATABASECHANGELOGLOCK;

1

2

一般情况下是本机锁住的；则通过下面sql解锁

UPDATE DATABASECHANGELOGLOCK

SET locked=0, lockgranted=null, lockedby=null

WHERE id=1



