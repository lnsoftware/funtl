# [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#itoken-项目简介)iToken 项目简介

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#本节视频)本节视频

- [【视频】项目实战-iToken-项目简介](https://www.bilibili.com/video/av28182645)

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#开发环境)开发环境

- 操作系统：Windows 10 Enterprise
- 开发工具：Intellij IDEA
- 数据库：MySQL 5.7.22
- Java SDK：Oracle JDK 1.8.152

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#部署环境)部署环境

- 操作系统：Linux Ubuntu Server 16.04 X64
- 虚拟化技术：VMware + Docker

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#项目管理工具)项目管理工具

- 项目构建：Maven + Nexus
- 代码管理：Git + GitLab
- 镜像管理：Docker Registry

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#后台主要技术栈)后台主要技术栈

- 核心框架：Spring Boot + Spring Cloud
- 视图框架：Spring MVC
- 页面引擎：Thymeleaf
- ORM 框架：tk.mybatis 简化 MyBatis 开发
- 数据库连接池：Alibaba Druid
- 数据库缓存：Redis Sentinel
- 消息中间件：RabbitMQ
- 接口文档引擎：Swagger2 RESTful 风格 API 文档生成
- 全文检索引擎：ElasticSearch
- 分布式链路追踪：ZipKin
- 分布式文件系统：Alibaba FastDFS
- 分布式服务监控：Spring Boot Admin
- 分布式协调系统：Spring Cloud Eureka
- 分布式配置中心：Spring Cloud Config
- 分布式日志系统：ELK（ElasticSearch + Logstash + Kibana）
- 反向代理负载均衡：Nginx

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#前端主要技术栈)前端主要技术栈

- 前端框架：Bootstrap + jQuery
- 前端模板：AdminLTE

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#自动化运维)自动化运维

- 持续集成：GitLab
- 持续交付：Jenkins
- 容器编排：Kubernetes

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#系统架构)系统架构

![img](https://funtl.com/assets/Lusifer2018072916110001.png)

## [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#服务规划)服务规划

### [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#cloud)Cloud

| 服务名称      | 服务端口 | 服务说明       |
| ------------- | -------- | -------------- |
| itoken-eureka | 8761     | 服务注册与发现 |
| itoken-config | 8888     | 分布式配置中心 |
| itoken-zipkin | 9411     | 分布式链路追踪 |
| itoken-zuul   | 8769     | 分布式路由网关 |
| itoken-admin  | 8084     | 分布式系统监控 |

### [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#service)Service

| 服务名称                  | 服务端口 | 服务说明           |
| ------------------------- | -------- | ------------------ |
| itoken-service-admin      | 8501     | 管理员服务提供者   |
| itoken-service-redis      | 8502     | 数据缓存服务提供者 |
| itoken-service-sso        | 8503     | 单点登录服务提供者 |
| itoken-service-posts      | 8504     | 文章服务提供者     |
| itoken-service-upload     | 8505     | 文件上传服务提供者 |
| itoken-service-digiccy    | 8506     | 数字货币服务提供者 |
| itoken-service-collection | 8507     | 数据采集服务提供者 |

### [#](https://funtl.com/zh/spring-cloud-itoken/iToken-项目简介.html#web)Web

| 服务名称           | 服务端口 | 服务说明           |
| ------------------ | -------- | ------------------ |
| itoken-web-admin   | 8601     | 管理员服务消费者   |
| itoken-web-posts   | 8602     | 文章服务消费者     |
| itoken-web-backend | 8603     | 后台服务聚合       |
| itoken-web-digiccy | 8604     | 数字货币服务消费者 |

上次更新: 2019-4-19 19:23:15

← [iToken 白皮书](https://funtl.com/zh/spring-cloud-itoken/微服务架构实战-iToken-白皮书.html)