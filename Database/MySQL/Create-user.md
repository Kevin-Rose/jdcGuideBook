# 1. mysql 创建用户

## 1.创建用户:

 指定ip：192.118.1.1的username用户登录

```
create user 'username'@'192.118.1.1' identified by 'password123';
```
指定ip：192.118.1.开头的username用户登录

```
create user 'username'@'192.118.1.%' identified by 'password123';
```
指定任何ip的commentsUserPro用户登录

```
create user 'commentsUserPro'@'%' identified by 'Y29tbWV&$100';
```
## 2.删除用户

```
drop user '用户名'@'IP地址';
```

## 3.修改用户

```
rename user '用户名'@'IP地址' to '新用户名'@'IP地址';
```
## 4.修改密码

set password for '用户名'@'IP地址'=Password('新密码');
SELECT * FROM mysql.user

#3.授权某个用户拥有某个数据库的所有权限

```
CREATE USER 'db_chatbot_admin_root'@'%' IDENTIFIED BY 'Y29tbWV&$100Y29tbWV&$100'; 
GRANT ALL PRIVILEGES  ON db_chatbot_admin.* TO "db_chatbot_admin_root"@'%';
```

```
SELECT *FROM`chat`.`chat_log_bi` 
  WHERE YEAR(STR_TO_DATE(`chat`.`chat_log_bi`.`Created Date`, '%Y-%m-%d %H'))=2021

## #4.刷
npm --registry https://registry.npm.taobao.org install
```

## 新权限

```
FLUSH PRIVILEGES;
ip:101.201.103.202
username:commentsUser
PASSWORD:Y29tbWVudHNfdXNlcg&$100
PORT:3306
```

# 2. 安装MySQL在Linux

