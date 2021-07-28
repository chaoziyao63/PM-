
# Spring Cloud应用接入zookeeper-cvm部署场景
## 操作场景
本文介绍如何将通过tem部署的Spring Cloud 应用接入微服务引擎托管的zookeeper注册中心。接入无需修改任何代码。
## 操作步骤

1.在[腾讯云弹性微服务控制台](https://console.cloud.tencent.com/tem)中创建环境。具体操作请参见[创建环境](https://cloud.tencent.com/document/product/1371/53293)。

2.在[腾讯云微服务引擎控制台](https://console.cloud.tencent.com/tse)创建zookeeper注册中心实例。具体操作请参见[创建微服务引擎实例](https://cloud.tencent.com/document/product/1364/58416)。

<dx-alert infotype="explain" title="">
创建zookeeper注册中心实例时，若不开启公网访问，则所选定的VPC需要与tem已创建的环境的VPC保持一致。
</dx-alert>

3.在环境中一键关联TSE中的Zookeeper注册中心。


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


