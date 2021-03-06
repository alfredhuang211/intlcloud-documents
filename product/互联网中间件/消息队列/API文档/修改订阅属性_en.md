## 1. API Description

This API (SetSubscriptionAttributes) is used to modify the attributes of a subscription.

Domain for public network API request: <font style="color:red">cmq-topic-region.api.qcloud.com</font>

Domain for private network API request: <font style="color:red">cmq-topic-region.api.tencentyun.com</font>

> At any time (including alpha test), any downstream traffic generated when using public network domain will incur traffic fee. It is strongly recommended that users on Tencent Cloud use **private network** domain, as it will not incur any traffic fee.

- The "region" should be replaced by a specific region: gz (Guangzhou), sh (Shanghai), bj (Beijing). The "region" value in the common parameter should be kept consistent with that in the domain. In case of inconsistency, the one in the domain should prevail. The request should be sent to the region specified by the domain.
- Requests for accessing via public network domain support both HTTP and HTTPS. Requests for accessing via private network only support HTTP.
- Some of the input parameters are optional, so the default values are not required.
- All output parameters will be returned to the user when the request is successful; otherwise, at least code, message, and requestId will be returned.

## 2. Input Parameters

The following request parameter list only provides API request parameters. For other parameters, refer to [Common Request Parameters](https://cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| topicName | Yes | String | Topic name. It is unique under the same account in a single region. Topic name is a string with no more than 64 characters. It must start with letter, and the rest may contain letters, numbers and dashes (-). |
| subscriptionName | Yes | String | Subscription name. It is unique for the same topic under the same account in a single region. Subscription name is a string with no more than 64 characters. It must start with letter, and the rest may contain letters, numbers and dashes (-). |
| protocol | No | String | Subscription protocol. Currently, two types of protocols are supported: HTTP, queue. When using HTTP protocol, users need to build web server to receive messages on their own. When using queue, messages will be automatically pushed to the CMQ queue and users can pull the messages concurrently. |
| endpoint | No | String | endpoint used to receive notification. It varies with the protocol: for HTTP, endpoint must start with "http://", and host can be either domain or IP; for queue, queueName is entered here. |
| notifyStrategy | No | String | Retry policy for the CMQ push server in case of errors when pushing messages to the endpoint. Available values are: 1) BACKOFF_RETRY (backoff retry). Re-push the message at regular intervals. Discard the message after a certain number of reties have been committed, then continue pushing the next message; 2) EXPONENTIAL_DECAY_RETRY (exponential decay retry). The interval between retries is increased exponentially, for example, retry in 1s first, then 2s, 4s, 8s...Since the cycle of a Topic message is one day, the retry operations will last for at most one day before the message is discarded. Default is EXPONENTIAL_DECAY_RETRY. |
| notifyContentFormat | No | String | Notification content format. Available values are: 1) JSON; 2) SIMPLIFIED, i.e. raw format. If the protocol is queue, the value must be SIMPLIFIED. If the protocol is HTTP, both values are available. Default is JSON. |
| filterTag.n | No | String | Message body. Message tag (used to filter message). There can be up to 5 tags, each containing no more than 16 characters. It is used in combination with the msgTag parameter of [(Batch)PublishMessage](https://cloud.tencent.com/document/api/406/7411). Rules: 1) If filterTag is not configured, the subscribers will receive all the messages published on Topic no matter whether msgTag is configured or not; 2) If filterTag array is configured with values, the subscribers will receive messages published on Topic only if at lease one of the values in the array exists in the msgTag array as well (that is, filterTag and msgTag intersect with each other); 3) If filterTag array is configured with values but msgTag is not configured, the subscribers will not receive any messages published on Topic. This can be considered a special case of 2), when there is no intersection between filterTag and msgTag. The design concept of the rules is based on the wills of the subscribers. |
| bindingKey.n | Yes | String Array | There can be up to 5 bindingKeys, each with a length limit of 64 Bytes. This field indicates the filtering policy used for the subscribers to receive messages. Each bindingKey may contain up to 15 ".", i.e. 16 phrases at most. |
## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | 0: Succeeded, others: Error. For detailed errors, please refer to the table below. |
| message | String | Error message. |
| requestId | String | ID of the request generated by server. When there is an internal error on the server, users can submit this ID to backend to locate the problem. |

<table class="t">
<tbody><tr>
<th> <b>Error Code</b>
</th><th> <b>Module Error Code</b>
</th><th> <b>Error Message</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> 4000
</td><td> 10490
</td><td> number of filterTag exceed limit
</td><td> The number of filterTag exceeded the limit. Currently, the limit is 5.
</td></tr>
<tr>
<td> 4000
</td><td> 10520
</td><td> undefined notify retry stragety
</td><td> Undefined push notification retry policy. Please check for spelling errors.
</td></tr>
<tr>
<td> 4000
</td><td> 10530
</td><td> undefined notify content format
</td><td> Undefined push notification format. Please check for spelling errors.
</td></tr>

</tbody></table>

Note: The error codes listed in the above table are specific to the API. If the error code you are looking for is not here, you may find it in the [Common Error Codes](https://intl.cloud.tencent.com/document/product/406/5903).

## 4. Example

Input:

```
 https://domain/v2/index.php?Action=SetSubscriptionAttributes
 &topicName=test-Topic-123
 &subscriptionName=test-subscription-123
 &filterTag.0=football
 &<Common request parameters>
```

Output:

```
{
"code" : 0,
"message" : "",
"requestId":"14534664555"
}
```







