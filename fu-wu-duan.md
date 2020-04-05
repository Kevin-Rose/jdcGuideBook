一、项目介绍    3

1、项目简介    3

2、项目目录结构说明    5

3、    系统架构部署图    6

二、技术选型    7

1、    后端架构    7

2、    前端架构    7

三、开发环境    8

1、开发环境工具介绍    8

2、前端接口    9

四、    项目部署    9

1、    域名配置    9

2、    项目部署目录    11

3、    Nginx配置    11

4、    微服务启动顺序    12

5、    日志查看    12

一、项目介绍

1、项目简介

功能点：

```
    简单采商城，完整的购物流程、后端运营平台对前端业务的支撑，和对项目的运维，有各项的监控指标和运维指标。
```

技术点：

```
   核心技术为springcloud+vue两个全家桶实现，整体技术栈只有阿里云短信服务和七牛云存储是收费的，所用的技术都是目前java前瞻性的框架，可以为中小企业解决微服务架构难题，可以帮助企业快速建站。本项目由10个后端项目和3个前端项目共同组成。真正实现了基于RBAC、jwt和oauth2的无状态统一权限认证的解决方案，实现了异常和日志的统一管理，实现了MQ落地保证100%到达的解决方案。



核心框架：springcloud Edgware全家桶

安全框架：Spring Security Spring Cloud Oauth2

分布式任务调度：elastic-job

持久层框架：MyBatis、通用Mapper4、Mybatis\_PageHelper

数据库连接池：Alibaba Druid

日志管理：Logback    前端框架：Vue全家桶以及相关组件
```

三方服务： 邮件服务、阿里云短信服务、七牛云文件服务

2、项目目录结构说明

3、    系统架构部署图

二、技术选型

1、    后端架构

1\)    spring cloud Eureka

服务注册中心

2\)    Spring Cloud config

配置中心

3\)    spring cloud security

安全认证

4\)    Spring Cloud Feign

服务提供和消费

5\)    Spring Cloud Zuul

微服务网关

6\)    Spring Cloud Hystrix

7\)    Spring Cloud Turbine

8\)    spring Cloud Sleuth Zipkin

9\)    Spring Cloud Stream

10\)    Binder Rabbit

11\)    Spring Cloud Oauth2

12\)    Spring Boot

13\)    Spring Boot Mail

14\)    MyBatis

15\)    Mybatis\_PageHelper

16\)    RabbitMQ

17\)    RocketMQ

18\)    MySQL

19\)    Redis

20\)    Zookeeper

21\)    阿里云短信服务

22\)    七牛云文件服务

。。。

2、     前端架构

Vue全家桶技术栈

三、开发环境

1、开发环境工具介绍

1\)    Mysql

版本：5.6.41

下载地址：[https://www.mysql.com/](https://www.mysql.com/)

安装路径：系统默认目录

2\)    Redis

版本：4.0.11

下载地址：[https://redis.io/](https://redis.io/)

安装路劲：/root/web/tool

3\)    nginx

版本：nginx/1.12.2

下载地址：[http://nginx.org/en/download.html](http://nginx.org/en/download.html)

安装路劲：系统默认目录

4\)    rocketmq

版本：  4.3.0

下载地址：[http://rocketmq.apache.org/](http://rocketmq.apache.org/)

安装路劲：/root/web/tool

5\)    zookeeper

版本：3.4.12

下载地址：[https://zookeeper.apache.org/](https://zookeeper.apache.org/)

安装路劲：/root/web/tool

6\)    rabbitmq

版本：3.7.23

下载地址：[https://www.rabbitmq.com/](https://www.rabbitmq.com/)

安装路劲：/root/web/tool

7\)    nexus私服

版本：3.14.0

下载地址：[https://www.sonatype.com/nexus-repository-oss](https://www.sonatype.com/nexus-repository-oss)

安装路劲：/root/web/tool

访问路径：[http://47.95.217.226:8081/](http://47.95.217.226:8081/)

注： 各个工具的详细配置及账号密码 请参考各个工具安装目录的配置文件和项目代码。

2、前端接口

前端接口参考用户端和管理端接口文档

四、    项目部署

1、    域名配置

配置文件路劲：/etc/hosts

2、    项目部署目录

因为目前服务器有限并没有分布式部署，所以全部部署在 /data/logs/jdc

3、    Nginx配置

配置文件路劲：/etc/nginx/nginx.conf

4、    微服务启动顺序

1\)    jdc-eureka

2\)    jdc-discovery

3\)    jdc-provider-uac

4\)    jdc-gateway

5\)    剩下微服务无启动数序要求

5、    日志查看

各个微服务项目日志文件的路径：/data/logs/jdc/ + 微服务名





