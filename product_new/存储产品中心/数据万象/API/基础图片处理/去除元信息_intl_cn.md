## 功能概述

腾讯云数据万象通过 **imageMogr2** 接口可去除图片元信息，包括 exif 信息。

## 接口形式
```
download_url?imageMogr2/strip
```

## 参数说明

操作名称：strip。

| 参数         | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | 文件的访问链接<br>具体构成为`<BucketName-APPID>.<picture region>.<domain>.com/<picture name>`<br>例如 `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`。 

## 示例

**去除元信息**
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/strip	