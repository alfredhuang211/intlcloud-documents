The common parameters are used to authenticate the user and API. If not necessary, these parameters are not described in individual API documents. However, they have to be carried by each request to initiate properly.

## Signature Algorithm v3

When the TC3-HMAC-SHA256 algorithm algorithm is used, the common parameters should be uniformly placed in the HTTP request header as shown below:

| Parameter Name | Type | Required | Description |
|--------|----|----|----|
| X-TC-Action | String | Yes | The name of the API for the desired operation. For the specific value, see the description of common parameter Action in the input parameters in related API documentation. For example, the API for querying CVM instance list is DescribeInstances.
| X-TC-Region | String | Yes | Region parameter, which is used to identify the region to which the data you want to work with belongs. For values supported for an API, see the description of common parameter Region in the input parameters in related API documentation. Note: This parameter is not required for some APIs (which will be indicated in related API documentation), and will not take effect even it is passed. |
| X-TC-Timestamp | Integer | Yes | The current UNIX timestamp that records the time when the API request was initiated, for example, 1529223702. Note: If the difference between the UNIX timestamp and the server time is greater than 5 minutes, a signature expiration error may occur. |
| X-TC-Version | String | Yes | The version of the API for the desired operation. For the specific value, see the description of common parameter Version in the input parameters in related API documentation. For example, 2017-03-12. |
| Authorization | String | Yes | Header field of HTTP standard identity authentication, such as: <br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024 <br/> Here: <br/>- TC3-HMAC-SHA256: Signature algorithm. This value is always used. <br/>- Credential: Signature credentials. AKIDEXAMPLE is SecretId. Date is UTC date, which must be consistent with the UTC date converted by the X-TC-Timestamp common parameter. service is the product name, which is generally a domain name prefix; for example, domain name cvm.tencentcloudapi.com means that the product name is CVM, and the value for this product is as; <br/>- SignedHeaders: Header information for signature calculation. The content-type and host are required; <br/>- Signature: signature digest. |
| X-TC-Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |

Assume that you want to query the list of Cloud Virtual Machine instances in the Guangzhou region, structure a request that consists of the request URL, the request header and request body as follows:

The following example shows you how to structure an HTTP GET request:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

Example of an HTTP POST (application/json) request structure:

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: application/json
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

{"Offset":0,"Limit":10}
```

Example of an HTTP POST (multipart/form-data) request structure (only supported by specific APIs):

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: multipart/form-data; boundary=58731222010402
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

--58731222010402
Content-Disposition: form-data; name="Offset"

0
--58731222010402
Content-Disposition: form-data; name="Limit"

10
--58731222010402--
```

## Signature Algorithm v1

When using HmacSHA1 or HmacSHA256 to sign your requests, you should include all common parameters in the HTTP header as shown below:

| Parameter Name | Type | Required | Description |
|:---------|:---------|:-----|:---- |
| Action | String | Yes | The name of the API for the desired operation. For the specific value, see the description of common parameter Action in the input parameters in related API documentation. For example, the API for querying CVM instance list is DescribeInstances.
| Region | String | Yes | Region parameter, which is used to identify the region to which the data you want to work with belongs. For values supported for an API, see the description of common parameter Region in the input parameters in related API documentation. Note: This parameter is not required for some APIs (which will be indicated in related API documentation), and will not take effect even it is passed. |
| Timestamp | Integer | Yes | The current UNIX timestamp that records the time when the API request was initiated, for example, 1529223702. If the difference between the value and the current system time is too large, a signature expiration error may occur. |
| Nonce | Integer | Yes | A random positive integer used in conjunction with Timestamp to prevent replay attacks |
| SecretId | String | Yes | The identifying SecretId obtained on the [TencentCloud API Key](https://console.cloud.tencent.com/capi) page. A SecretId corresponds to a unique SecretKey which is used to generate the request signature (Signature). |
| Signature | String | Yes | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information on how to compute the signature, see the documentation about API authentication. |
| Version | String | Yes | The version of the API for the desired operation. For the specific value, see the description of common parameter Version in the input parameters in related API documentation. For example, 2017-03-12. |
| SignatureMethod | String | No | Signature algorithm. Currently, only HmacSHA256 and HmacSHA1 are supported. The HmacSHA256 algorithm is used to verify the signature only when this parameter is specified as HmacSHA256. In other cases, the signature is verified with HmacSHA1. |
| Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |


Assume that you want to query the list of Cloud Virtual Machine instances in the Guangzhou region, structure a request that consists of the request URL, the request header and request body as follows:

The following example shows you how to structure an HTTP GET request:
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```

The following example shows you how to structure an HTTP POST request:

```
https://cvm.tencentcloudapi.com/

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded

Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
```


## Region List

The supported Region field values for all APIs in this product are listed as below. For any API that does not support any of the following regions, this field will be described additionally in the relevant API document.


| Region | Value |
|------|------|
|Asia Pacific (Bangkok)|ap-bangkok|
|North China (Beijing)|ap-beijing|
|Southwest China (Chengdu)|ap-chengdu|
|Southwest China (Chongqing)|ap-chongqing|
|South China (Guangzhou)|ap-guangzhou|
|Southeast Asia (Hong Kong, China)|ap-hongkong|
|Asia Pacific (Mumbai)|ap-mumbai|
|Asia Pacific (Seoul)|ap-seoul|
|East China (Shanghai)|ap-shanghai|
|East China (Shanghai Finance)|ap-shanghai-fsi|
|South China (Shenzhen Finance)|ap-shenzhen-fsi|
|Southeast Asia (Singapore)|ap-singapore|
|Asia Pacific (Tokyo)|ap-tokyo|
| Europe (Frankfurt) | eu-frankfurt |
|Europe (Moscow)|eu-moscow|
|East US (Virginia)|na-ashburn|
|West US (Silicon Valley)|na-siliconvalley|
|North America (Toronto)|na-toronto|
