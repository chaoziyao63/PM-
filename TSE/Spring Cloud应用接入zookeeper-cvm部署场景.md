
# Spring Cloud应用接入zookeeper-cvm部署场景
## 操作场景
本文介绍如何将通过cvm部署的Spring Cloud 应用接入微服务引擎托管的zookeeper注册中心。接入无需修改任何代码。
## 操作步骤

1.在[CVM控制台](https://console.cloud.tencent.com/cvm)创建CVM实例。具体操作请参见[CVM实例创建指引](https://cloud.tencent.com/document/product/213/44264)。

2.准备Spring Cloud应用Jar包。我们同时为您提供了Spring Cloud应用demo代码库：
[Demo 代码仓库 >>](https://github.com/tencentyun/tse-simple-demo)

3.上传Spring Cloud应用Jar包至CVM实例。

4.在[TSE控制台](https://console.cloud.tencent.com/tse)创建zookeeper注册中心实例。具体操作请参见[创建微服务引擎实例](https://cloud.tencent.com/document/product/1364/58416)。

<dx-alert infotype="explain" title="">
创建zookeeper注册中心实例时，若不开启公网访问，则所选定的VPC需要与CVM实例的VPC保持一致。
</dx-alert>

5.zookeeper注册中心实例创建成功后，在[TSE控制台](https://console.cloud.tencent.com/tse)获取 TSE Zookeeper注册中心实例访问IP。

6.指定注册中心地址参数并运行该应用。登录至 CVM 实例中，运行以下命令：

```
nohup java 
-Dspring.cloud.zookeeper.connect-string=[TSE Zookeeper注册中心实例访问IP:2181]
-jar [jar包名称] &
```

7.在[TSE控制台](https://console.cloud.tencent.com/tse)验证服务注册。点击进入注册中心实例的服务管理页面，若出现以下页面，则证明服务注册成功。
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


