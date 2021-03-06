腾讯云服务器 CVM（Cloud Virtual Machine）是腾讯云提供的可扩展的计算服务。使用 CVM 避免了使用传统服务器时需要预估资源用量及前期投入，帮助您在短时间内快速启动任意数量的云服务器并即时部署应用程序。
腾讯云 CVM 支持用户自定义一切资源：CPU、内存、硬盘、网络、安全等等，并可以在需求发生变化时轻松地调整它们。

## 相关概念

使用腾讯云服务器 CVM 之前，您还需要了解以下概念：
- **实例**：云端的虚拟计算资源，包括 CPU、操作系统、网络、磁盘等最基础的计算组件。
- **实例类型**：腾讯云提供的云服务器的各种不同 CPU、内存、存储和网络配置。可以参考 [实例规格](http://intl.cloud.tencent.com/document/product/213/11518) 了解更多。
- **镜像**：指云服务器 CVM 运行的预制模版，包括预配置的操作系统及预装软件。腾讯云 CVM 提供 Windows，Linux 等多种预制镜像。
- **本地盘**：与实例处于同一台物理服务器上的，可被实例用作持久存储的设备。
- **云硬盘**：提供的分布式持久块存储设备，可以用作实例的系统盘或可扩展数据盘使用。
- **私有网络**：腾讯云提供的虚拟的隔离的网络空间，与其他资源逻辑隔离。
- **IP地址**：腾讯云提供 [内网 IP ](http://intl.cloud.tencent.com/document/product/213/5225) 和 [公网 IP](http://intl.cloud.tencent.com/document/product/213/5224)。简单理解，内网 IP 提供局域网（LAN）服务，云服务器之间互相访问。公网 IP 在用户在云服务器实例上需要访问 Internet 服务时使用。
- **弹性IP**：专为动态网络设计的静态公网 IP，满足快速排障需求。
- **安全组**：安全组可以理解为是一种虚拟防火墙，具备状态检测和数据包过滤功能，用于一台或者多台云服务器网络访问控制，安全组是重要的网络安全隔离手段。
- **登录方式**：安全性高的 [SSH 密钥对](http://intl.cloud.tencent.com/document/product/213/6092) 和普通密码的 [登录密码](http://intl.cloud.tencent.com/document/product/213/6093)。
- **地域和可用区**：实例和其他资源的启动位置。
- **腾讯云控制台**：基于 Web 的用户界面。


## 如何使用云服务器 

腾讯云提供如下方式进行云服务器的配置和管理：

- **控制台**：腾讯云提供的 Web 服务界面，用于配置和管理云服务器。
- **API**：腾讯云也提供了 API 接口方便您管理云服务器 CVM。关于 API 说明，请参考 [API 概览](https://intl.cloud.tencent.com/document/product/213/15688)。
- **SDK**：您可以使用 [SDK 编程](https://intl.cloud.tencent.com/document/product/494) 或使用腾讯云 [命令行 CLI](https://intl.cloud.tencent.com/document/product/1013/30220) 工具调用 CVM API。



## 快速购买及配置云服务器

如果您是个人用户并且首次购买云服务器，腾讯云推荐您通过我们提供的快速入门配置方案，可参考：
- [快速入门 Windows 云服务器](http://intl.cloud.tencent.com/document/product/213/2764)
- [快速入门 Linux 云服务器](http://intl.cloud.tencent.com/document/product/213/2936)

如果您对云服务器配置有更高配置的需求，例如对于存储介质、容量、网络带宽以及安全组设置的自定义配置，可参考：
- [自定义配置 Windows 云服务器](http://intl.cloud.tencent.com/document/product/213/10516)
- [自定义配置 Linux 云服务器](http://intl.cloud.tencent.com/document/product/213/10517)

## CVM 定价

CVM 定价，请参考 [CVM Pricing (Linux)](https://intl.cloud.tencent.com/document/product/213/30011)。

## 其他相关产品

- 您可以使用弹性伸缩定时或根据条件地自动增加及减少服务器集群数量。更多信息，请参考 [弹性伸缩产品文档](https://intl.cloud.tencent.com/document/product/377)。
- 您可以使用负载均衡横跨多个云服务器实例自动分配来自客户端的请求流量。更多信息，请参考 [负载均衡产品文档](https://intl.cloud.tencent.com/document/product/214)。
- 您可以使用容器服务管理在一组云服务器的应用生命周期。更多信息，请参考 [容器服务产品文档](https://intl.cloud.tencent.com/document/product/457)。
- 您可以使用云监控服务监控云服务器实例及其系统盘。更多信息，请参考 [云监控产品文档](https://intl.cloud.tencent.com/document/product/248)。
- 您可以在云上部署关系数据库，也可以使用腾讯云云数据库。更多信息，请参考 [云数据库 MySQL](https://intl.cloud.tencent.com/document/product/236)。


