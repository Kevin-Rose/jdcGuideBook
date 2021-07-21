cd .. && cd u01 && rm -rf s*jar  && rz &&  java -jar  s*.jar

java -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,address=9094,suspend=n,server=y -jar s*.0.jar





cd .. && cd u01 && rm -rf s*jar  && rz &&  java -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,address=9094,suspend=n,server=y -jar s*.0.jar

