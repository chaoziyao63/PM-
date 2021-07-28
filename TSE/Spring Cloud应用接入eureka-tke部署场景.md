# Spring Cloud应用接入zookeeper-tke部署场景
## 操作场景
本文介绍如何将通过tke部署的Spring Cloud 应用接入微服务引擎托管的eureka注册中心。接入无需修改任何代码。
## 操作步骤

1.在[TKE控制台](https://console.cloud.tencent.com/tke)中创建TKE容器集群。具体操作请参见[创建TKE集群](https://cloud.tencent.com/document/product/457/32189)。

2.准备Spring Cloud应用镜像文件。我们同时为您提供了Spring Cloud应用demo代码库：
[Demo 代码仓库 >>](https://github.com/tencentyun/tse-simple-demo)

3.上传Spring Cloud应用镜像文件至TKE镜像仓库。具体操作请参见[镜像仓库快速入门](https://cloud.tencent.com/document/product/1141/50332#null)。

4.在[TSE控制台](https://console.cloud.tencent.com/tse)创建eureka注册中心实例。具体操作请参见[创建eureka实例](https://cloud.tencent.com/document/product/1364/58416)。

<dx-alert infotype="explain" title="">
创建eureka注册中心实例时，若不开启公网访问，则所选定的VPC需要与TKE容器集群的VPC保持一致。
</dx-alert>

5.eureka注册中心实例创建成功后，在[TSE控制台](https://console.cloud.tencent.com/tse)获取 TSE Eureka注册中心实例访问IP。

6.在TKE容器集群中创建工作负载并选择对应镜像文件。具体操作请参见[Deployment管理](https://cloud.tencent.com/document/product/457/31705)。

<dx-alert infotype="explain" title="">
创建工作负载时，需将环境变量JAVA_OPTS指定为-Dspring.cloud.zookeeper.connect-string=[TSE Zookeeper注册中心实例访问IP:2181]
</dx-alert>

7.验证服务注册。点击进入注册中心实例的服务管理页面，若出现以下页面，则证明服务注册成功。
![](https://main.qcloudimg.com/raw/2f9befc1fee7efbbcd30542cbf3728fb.png)
## 注意事项
Spring Cloud 应用接入Zookeeper 注册中心，配置文件格式需如下所示：

```
spring:
  cloud:
    zookeeper:
      connect-string: [zookeeper注册中心IP:2181]
      discovery:
        register: true
        enabled: true
        prefer-ip-address: true
```
