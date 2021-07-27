# Spring Cloud应用接入zookeeper-tke部署场景
## 操作场景
本文介绍如何将通过tke部署的Spring Cloud 应用接入微服务引擎托管的zookeeper注册中心。接入无需修改任何代码。
## 前提条件
1.已创建TKE容器集群。具体操作请参见[创建TKE集群](https://cloud.tencent.com/document/product/457/32189)。

2.已准备Spring Cloud应用镜像文件。我们同时为您提供了Spring Cloud应用demo代码库：
[Demo 代码仓库 >>](https://github.com/tencentyun/tse-simple-demo)

3.已上传Spring Cloud应用镜像文件至TKE镜像仓库。具体操作请参见[镜像仓库快速入门](https://cloud.tencent.com/document/product/1141/50332#null)。

4.已在TKE容器集群中创建工作负载并选择对应镜像文件。具体操作请参见[Deployment管理](https://cloud.tencent.com/document/product/457/31705)。
<dx-alert infotype="explain" title="">
创建工作负载时，需将环境变量JAVA_OPTS指定为-Dspring.cloud.zookeeper.connect-string=[zookeeper注册中心IP:2181]
</dx-alert>


5.已在[腾讯云微服务引擎控制台](https://console.cloud.tencent.com/tse)创建zookeeper注册中心实例，且该注册中心实例与上传应用的TKE容器集群处于同一VPC内。具体操作请参见[创建微服务引擎实例](https://cloud.tencent.com/document/product/1364/58416)。
## 操作步骤
### 1. 获取 TSE Zookeeper注册中心实例访问地址
可以在[腾讯云微服务引擎控制台](https://console.cloud.tencent.com/tse)复制。
### 2. 修改注册中心地址参数
修改工作负载yaml文件中的环境变量JAVA_OPTS，将zookeeper注册中心IP替换为为TSE托管的Zookeeper注册中心的IP。

### 3. 验证服务注册
点击进入注册中心实例的服务管理页面，若出现以下页面，则证明服务注册成功。
<img src="https://main.qcloudimg.com/raw/634875f23e5d4841095fe512d2809446.png">

## 注意事项
Spring Cloud 应用需要使用如下的配置接入Zookeeper 注册中心：

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
