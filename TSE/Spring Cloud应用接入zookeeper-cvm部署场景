# Spring Cloud应用接入zookeeper-cvm部署场景
## 操作场景
本文介绍如何将cvm部署的Spring Cloud 应用接入微服务引擎托管的zookeeper注册中心。接入无需修改任何代码。
## 前提条件
1.已创建CVM实例。具体操作请参见[CVM实例创建指引](https://cloud.tencent.com/document/product/213/44264)。
2.已准备Spring Cloud应用Jar包。我们同时为您提供了Spring Cloud应用demo代码库：
[Demo 代码仓库 >>](https://github.com/tencentyun/tse-simple-demo)
3.已上传Spring Cloud应用Jar包至CVM实例。
4.已在[腾讯云微服务引擎控制台](https://console.cloud.tencent.com/tse)创建zookeeper注册中心实例，且该注册中心实例与上传应用的CVM实例处于同一VPC内。具体操作请参见[创建微服务引擎实例](https://cloud.tencent.com/document/product/1364/58416)。
## 操作步骤
### 1. 获取 TSE 注册中心实例访问地址
可以在[腾讯云微服务引擎控制台](https://console.cloud.tencent.com/tse)复制。
### 2. 设置注册中心地址参数并运行该应用
登录至 CVM 实例中，运行以下命令：

```
nohup java 
-Dspring.cloud.zookeeper.connect-string=[TSE-Zookeeper注册中心IP]:2181 
-jar [jar包名称] &
```
### 3. 验证服务注册
点击进入注册中心实例的服务管理页面，若出现以下页面，则证明服务注册成功。
<img src="https://main.qcloudimg.com/raw/634875f23e5d4841095fe512d2809446.png">

## 注意事项
Spring Cloud 应用需要使用如下的配置接入Zookeeper 注册中心：

```
spring:
  cloud:
    zookeeper:
      connect-string: x.x.x.x:2181
      discovery:
        register: true
        enabled: true
        prefer-ip-address: true
```
