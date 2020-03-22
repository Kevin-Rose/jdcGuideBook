# [jenkins+github配置](https://www.cnblogs.com/jdm532000/p/7445205.html)

一、jenkins安装

1.下载jenkins.war

2.（安装好jdk）

3.启动jenkins.war：cmd---java -jar jenkins.war

4.选择安装插件Install suggested plugins

5.设置账号和密码，完成jenkins安装

二、github token生成

6.生成token：登录github---Setting---Personal Access Token---Generate new token（添加有读写权限的token：勾选repo和admin：repo\_hook）

7.github hook设置：github---要构建的项目---Setting---Webhooks---增加一个webhook（Payload URL输入jenkins访问url）

三、jenkins配置

8.jenkins github server配置：系统管理---系统设置---GitHub---Add GitHub Sever---\(Credentials\)Add---Kind选择“secret text”---Secret输入步骤6中生成的token---Test connetion，测试是否配置成功

三、构建项目

构建一个自由风格的软件项目url

9.General设置：输入项目名称，project url输入github上项目网址

10.源码管理：选择git---repository url\(github上---项目---Clone or download\)---credential（添加一个github读写权限的账号：Kind选择Username with password）---源码库浏览---选择githubweb---URL输入git上项目网址

11.构建触发器：选择GitHub hook trigger for GITScm polling

12.构建环境：选择Use secret text\(s\) or file\(s\)---Add---secret text，选择之前添加的那个secret text

13.保存

14.构建项目，测试是否成功

