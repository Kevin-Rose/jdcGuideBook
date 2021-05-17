### 一、安装JDK

```
 一般centos7都会自动默认安装好JDK.如果想自己安装想要的版本，可以卸载重新安装,这里就不讲了
```

### 二、下载maven

```
 下载命令：  wget http://mirrors.hust.edu.cn/apache/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz
```

![](https://img-blog.csdnimg.cn/2019062814122911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2d1YW5nemhvdTAwN19qYXZh,size_16,color_FFFFFF,t_70)

```
下载完成后，就可以在目录上有maven的压缩包：
```

![](https://img-blog.csdnimg.cn/20190628141405628.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2d1YW5nemhvdTAwN19qYXZh,size_16,color_FFFFFF,t_70)

### 三、解压与相关配置

```
  解压命令：tar vxf apache-maven-3.5.4-bin.tar.gz
```

![](https://img-blog.csdnimg.cn/20190628141717547.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2d1YW5nemhvdTAwN19qYXZh,size_16,color_FFFFFF,t_70)

修改环境变量， 在/etc/profile中添加以下几行

MAVEN\_HOME=/usr/local/maven3  
export MAVEN\_HOME  
export PATH=${PATH}:${MAVEN\_HOME}/bin

执行命令：source /etc/profile使环境变量生效

![](/assets/import.png)

maven安装完成！！！



rm .{your

file

name

}.swp

