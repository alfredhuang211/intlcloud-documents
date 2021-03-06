# 腾讯云COS迁移教程

## 1. 操作场景

腾讯云COS间迁移时MSP将通过内网拉取源对象存储桶数据并保存到目标对象存储桶，不会产生额外费用。

下文将详细介绍腾讯云COS间迁移，应如何配置半托管公网迁移任务，实现数据迁移。

## 2. 前提条件

### 腾讯云对象存储COS

创建目标存储空间：

创建目标存储空间，用于存放迁移的数据。详情请参见[创建存储桶](https://intl.cloud.tencent.com/document/product/436/13309)。

创建用于迁移的子用户并授予相关权限：

1. 登陆腾讯云控制台。

2. 搜索 访问管理 或在账号信息下拉菜单中单击进入访问管理页面。

3. 在左导航栏中单击 用户 > 用户列表 进入用户列表页面。

4. 新建子用户，勾选编程访问及腾讯云控制台访问。

5. 搜索并勾选QcloudCOSAccessForMSPRole及QcloudCOSFullAccess策略。

6. 完成子用户创建并保存子用户名，访问登陆密码，SecretId，SecretKey。

 

> **说明：**
> 迁移服务也可以使用主账号操作，但是出于安全考虑，建议新建子用户并使用子用户API密钥进行迁移，迁移完成后删除。

 

## 3. 操作步骤

### 登录迁移服务平台

1. 登录 [迁移服务平台](https://console.cloud.tencent.com/msp/v2file) ，在左导航栏中单击进入迁移工具页面。

2. 找到【文件迁移工具】模块，单击【立即使用】，进入文件迁移工具配置页面。

### 新建迁移任务

1. 在文件迁移工具页面，单击【新建任务】，进入新建文件迁移任务界面，进行迁移参数的设置。

2. 设置迁移任务名称。
    此处设置的名称，将用于在任务列表中查看迁移状态和迁移进度。
    ![img](https://main.qcloudimg.com/raw/81725decffbebf4467b1f9c9b2abfb35.png)

3. 设置要迁移的文件来源。
    此处迁移源服务提供商应选择腾讯云COS，并在下方AccessKey，SecretKey文本框中输入先前新建用于迁移的腾讯云子用户SecretId，SecretKey。源对象存储桶列表可在填入密钥后点击下拉框右侧刷新按钮获取。
    ![img](https://main.qcloudimg.com/raw/424733ad9c344d826fd99b80f65f1c52.png)

4. 选择文件存储方式。
    根据迁移的需求，设定迁移后文件的存储方式，可以选择：标准存储、低频存储、保持原存储属性。
    ![img](https://main.qcloudimg.com/raw/2f1136773cd9168f914d541e70ec1280.png)

5. 选择 Header 设置。
    如果源桶中的文件设定了 Header/Tag 并且需要在迁移后保留，请选择保留或设置替换规则。
    ![img](https://main.qcloudimg.com/raw/60aa2765c97949d494adf96539c7908b.png)

6. 设定迁移规则。
    选择对指定桶中的全部文件进行迁移，或仅迁移指定前缀的文件。

7. 指定迁移任务的开始时间。
    如需在指定时间开始迁移，开启此开关并设定开始时间。

8. 设定最高并发数。
    各公有云厂商的对象存储都有最高并发限制。为确保业务稳定，请在迁移前与源厂商确认并设置最高迁移可用 QPS。
    ![img](https://main.qcloudimg.com/raw/6da4e7afa74b5acab93ca7b6add64d12.png)

9. 选择要迁移到的目标位置。
    在迁移目标信息中，输入用于迁移的腾讯云子用户SecretId，SecretKey。目标对象存储桶列表可在填入密钥后点击下拉框右侧刷新按钮获取。
    ![img](https://main.qcloudimg.com/raw/8762d73cf54b28226a544b0b1a6ceab9.png)

10. 指定迁移到目标桶的指定目录。

     - 保存到根目录： 直接将源桶中的文件按原始相对路径保存到目标桶的根目录。

     - 保存到指定目录**：将源桶中的文件保持原始相对路径保存到指定目录中。
   ![img](https://main.qcloudimg.com/raw/a35ef5e7a5c98af31203766945684e86.png)
   例如：
   源桶中的文件/a.txt，/dir/b.txt两个文件，文本框中填写“dest”，那么迁移后这两个文件在目标桶中的路径为：/dest/a.txt，/dest/dir/b.txt。
   如果文本框中填写dest/20180901，那么迁移后这两个文件在目标桶中的路径为：/dest/20180901/a.txt，/dest/20180901/dir/b.txt。
      > **注意：**
      >- 若迁移源与目标源有内容不同，名称相同的文件，建议在【同名文件】配置处选择【跳过（保留目标桶中已有的同名文件）】，系统默认选择   【覆盖（源桶中的文件会覆盖目标桶中的同名文件）】。
      >- 若在迁移过程中对象（文件）内容有变化，需要进行二次迁移。

11. 选择迁移模式。

**新建迁移任务后手动下载 Agent 启动迁移**：选择 Agent 模式迁移，用户在单击“新建并启动”后，将仅创建任务配置，需要用户手动下载 Agent 在迁移源一侧的服务器上部署之后才会正式启动迁移。Agent 模式适用于已有专线希望通过专线迁移的场景。
 ![img](https://main.qcloudimg.com/raw/36ca6e5fc6b7a6e23b21d8ce0015a217.png)

## 4. 预估文件迁移时间

迁移速度由迁移过程中涉及到的每一个环节的最低速度决定，同时受到网络传输速度和最大并发数影响。影响因素有：

| 影响因素               | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 迁出源的读取速度       | 数据源的读取速度因不同的服务商而不同，通常：   传输速度在50Mbps - 200Mbps之间。   文件读取并发在500 - 3000之间（大量小文件的传输受并发限制）。 |
| MSP 平台的传输速度     | MSP 平台提供最大200Mbps的迁移带宽。                          |
| 迁入目标位置的写入速度 | 腾讯云对象存储 COS：写入传输速度200Mbps，写入并发500 - 800之间。   整体迁移速度会是6MByte - 25MByte（即21GB/小时 - 87GB/小时）之间。 |

 
