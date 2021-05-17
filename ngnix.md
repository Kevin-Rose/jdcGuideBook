**nginx安装:**

1. ` yum install nginx`  

nginx重启: 

   2.     `nginx -s reload`

nginx -s reload ：修改配置后重新加载生效

nginx -s reopen ：重新打开日志文件  
nginx -t -c /path/to/nginx.conf 测试nginx配置文件是否正确

关闭nginx：  
nginx -s stop :快速停止nginx  
quit ：完整有序的停止nginx

其他的停止nginx 方式：

ps -ef \| grep nginx

kill -QUIT 主进程号 ：从容停止Nginx  
kill -TERM 主进程号 ：快速停止Nginx  
pkill -9 nginx ：强制停止Nginx

启动nginx:  
nginx -c /path/to/nginx.conf

平滑重启nginx：  
kill -HUP 主进程号

`[root@jdc /]# yum -y install httpd-tools`

默认情况下，nginx自带安装了`ngx_http_auth_basic_module`模块，我们只需要用第三方工具设置用户名、密码，保存到文件中，并在nginx配置中开启访问验证即可。

# 强制账号密码访问： {#强制账号密码访问：}

#### 1.安装 htpasswd {#1安装-htpasswd}

```
$ yum  -y install httpd-tool
```

#### 2.设置账号密码 {#2设置账号密码}

```
$ sudo htpasswd -c /etc/nginx/passwd username
```

1. 按照提示输入密码，就在/etc/nginx目录下的passwd中保存了账号密码

```
$ more passwd 
username:$apr1$b2RIEmiN$yxkWM7HUJb9VoyDyek4Kg0
```

## nginx配置开启验证 {#nginx配置开启验证}

在 nginx 配置文件中加上：

```
location / {
    auth_basic "What are you want to do?";
    auth_basic_user_file /usr/local/nginx/passwd;
}
```

nginx -s reload ：修改配置后重新加载生效



nginx -s reload  ：修改配置后重新加载生效

nginx -s reopen  ：重新打开日志文件  
nginx -t -c /path/to/nginx.conf   测试nginx配置文件是否正确

关闭nginx：  
nginx -s stop  :快速停止nginx  
         quit  ：完整有序的停止nginx

其他的停止nginx 方式：

ps -ef \| grep nginx

kill -QUIT 主进程号     ：从容停止Nginx  
kill -TERM 主进程号     ：快速停止Nginx  
pkill -9 nginx          ：强制停止Nginx

启动nginx:  
nginx -c /path/to/nginx.conf

平滑重启nginx：  
kill -HUP 主进程号

`[root@jdc /]# yum -y install httpd-tools`

默认情况下，nginx自带安装了`ngx_http_auth_basic_module`模块，我们只需要用第三方工具设置用户名、密码，保存到文件中，并在nginx配置中开启访问验证即可。

# 强制账号密码访问：

#### 1.安装 htpasswd

```
$ yum  -y install httpd-tool
```

#### 2.设置账号密码

```
$ sudo htpasswd -c /etc/nginx/passwd username
```

1. 按照提示输入密码，就在/etc/nginx目录下的passwd中保存了账号密码

```
$ more passwd 
username:$apr1$b2RIEmiN$yxkWM7HUJb9VoyDyek4Kg0
```

## nginx配置开启验证

在 nginx 配置文件中加上：

```
location / {
    auth_basic "What are you want to do?";
    auth_basic_user_file /usr/local/nginx/passwd;
}
```

nginx -s reload  ：修改配置后重新加载生效





nginx -s reload  ：

修改配置后重新加载生效

nginx -s reopen  ：重新打开日志文件  
nginx -t -c /path/to/nginx.conf   测试nginx配置文件是否正确

关闭nginx：  
nginx -s stop  :快速停止nginx  
         quit  ：完整有序的停止nginx

其他的停止nginx 方式：

ps -ef \| grep nginx

kill -QUIT 主进程号     ：从容停止Nginx  
kill -TERM 主进程号     ：快速停止Nginx  
pkill -9 nginx          ：强制停止Nginx

启动nginx:  
nginx -c /path/to/nginx.conf

平滑重启nginx：  
kill -HUP 主进程号

`[root@jdc /]# yum -y install httpd-tools`

默认情况下，nginx自带安装了`ngx_http_auth_basic_module`模块，我们只需要用第三方工具设置用户名、密码，保存到文件中，并在nginx配置中开启访问验证即可。

# 强制账号密码访问：

#### 1.安装 htpasswd

```
$ yum  -y install httpd-tool
```

#### 2.设置账号密码

```
$ sudo htpasswd -c /etc/nginx/passwd username
```

1. 按照提示输入密码，就在/etc/nginx目录下的passwd中保存了账号密码

```
$ more passwd 
username:$apr1$b2RIEmiN$yxkWM7HUJb9VoyDyek4Kg0
```

## nginx配置开启验证

在 nginx 配置文件中加上：

```
location / {
    auth_basic "What are you want to do?";
    auth_basic_user_file /usr/local/nginx/passwd;
}
```

nginx -s reload  ：修改配置后重新加载生效





