[//]: # (chinagitpath:XXXXX)

本文档主要介绍固件升级在控制台的使用方法，帮助用户快速使用固件升级服务。

### 添加固件
进入物联网通信控制台，单击左侧边栏【产品列表】，选择想要为之添加固件的产品，再切换到【固件列表】 TAB，单击【添加新固件】按钮。
- 固件版本仅支持英文字母、数字、点、下划线和中划线，长度限制1~32字符。
- 上传的固件文件必须为 bin 文件或 tar/gz/zip 包。
- 上传的固件文件大小不能超过 10M。
- 最多能够为每个产品上传 50 个固件，若继续上传则需要删除老的固件。

![](https://main.qcloudimg.com/raw/42e0b288cdb56948eb2ada33a789764f.png)

上传完成后，固件将显示在列表中。
![](https://main.qcloudimg.com/raw/5ad7da53f674d9a6d26b495fd2c91e0d.png)

### 单一设备升级
固件上传成功后，单击左侧边栏【固件升级】，选择想要升级固件的产品，根据下拉框中的固件版本号筛选设备列表。
- 下拉框中显示的版本号列表为控制台上传的固件版本号和设备上报的固件版本号并集。

- 本文在 testProduct 产品下创建了 testDevice0 设备，并使该设备通过 MQTT over TLS 非对称加密连接了物联网通信后台并上报了自己的固件版本“0.0.1”。

通过固件版本下拉列表筛选出上报了“0.0.1”的 testDevice0 设备，单击【升级固件】可对单个设备进行固件升级，该功能常用于灰度验证固件内容。
![](https://main.qcloudimg.com/raw/26422264b4628f24f11a7ff7cebdd688.png)

切换到【升级状态列表】 TAB，可查看当前设备升级的状态。
- 状态包含：设备离线、任务等待中、消息下发成功、下载中、下载完成、升级中、升级失败、升级成功。
- 若设备超过 15 分钟未上报升级完成状态，那么本次升级将被标记为超时失败。

![](https://main.qcloudimg.com/raw/154c8bae5be173a61826c61bc00be61e.png)
![](https://main.qcloudimg.com/raw/74061edf75fd436f3012a6f382e55fb5.png)
![](https://main.qcloudimg.com/raw/e93de2173d654ddc8e871ed4f3fa8ba6.png)
### 批量升级
固件上传成功后，点击左侧边栏【固件升级】，选择想要升级固件的产品，根据下拉框中的固件版本号筛选设备列表并点击【批量升级固件】按钮
![](https://main.qcloudimg.com/raw/48db77076fc849684c2eed7b4a7ff34a.png)

切换到【升级状态列表】 TAB，可查看批量升级的所有设备当前的升级状态
![](https://main.qcloudimg.com/raw/154c8bae5be173a61826c61bc00be61e.png)
