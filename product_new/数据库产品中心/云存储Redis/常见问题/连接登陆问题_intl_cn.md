### 云服务器与云数据库部署在同一区域上，如何连接 Redis？
云服务器与云数据库部署在相同区域上时，请使用内网访问，连接请参见 [连接指导](https://intl.cloud.tencent.com/document/product/239/9897)。

### 云服务器与云数据库部署在不同区域上，如何连接 Redis？
基础网络和 VPC 网络互通，请参见 [基础网络互通](https://intl.cloud.tencent.com/document/product/215/5002)。
VPC 网络之间互通，请参见 [对等连接](https://intl.cloud.tencent.com/document/product/215/5000)。

### 如何处理云数据库 Redis 无法 ping 通？ 
Redis 是默认禁`ping`的，可以使用 telnet 来检测连通性。

### 如何开通 Redis 的外网访问？ 
云数据库 Redis 暂时不支持外网访问。
如果需要支持外网访问，可通过带有外网的 CVM 通过 Iptable 代理的方式来实现。

### 如何设置 Redis 免密码登录？ 
目前不支持免密码登录。

