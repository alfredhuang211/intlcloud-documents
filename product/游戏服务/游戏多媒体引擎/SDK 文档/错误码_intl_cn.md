欢迎使用腾讯云游戏多媒体引擎 SDK 。为方便开发者调试和接入腾讯云游戏多媒体引擎产品 API，这里向您介绍适用于游戏多媒体引擎开发的错误码文档。

## 一般性错误
|错误码名称|错误码值|原因及建议方案|
|--------|-------|------------|
|AV_ERR_NET_REQUEST_FALLED |7004|网络请求失败，一般由网络状态不稳定引起，建议检查网络状态|
|AV_ERR_CHARGE_OVERDUE     |7005|账号欠费导致失败，需要在腾讯云控制台上查看是否欠费|
|AV_ERR_AUTH_FIALD         |7006|鉴权失败 有以下几个原因：1、appid 不存在或者错误，2、authbuff 鉴权错误，3、鉴权过期|
|AV_ERR_IN_OTHER_ROOM      |7007|已经在其它房间|
|AV_ERR_DISSOLVED_OVERUSER |7008|dau 计费，房间超过 90 分钟后解散|
|AV_ERR_NO_PERMISSION      |7009|要进行某个操作的时候，没有权限|
|AV_ERR_FILE_CANNOT_ACCESS |7010|无法访问文件|
|AV_ERR_FILE_DAMAGED       |7011|文件被损坏|
|AV_ERR_3DVOICE_ERR_FILE_DAMAGED       |7002|3D音效文件未加载成功|
|AV_ERR_3DVOICE_ERR_NOT_INITED       |7003|需要先调用 InitSpatializer 接口|


## 客户端错误
|错误码名称     |错误码值|含义           |原因          |建议方案       |
|--------|----|-------|--------------------|-------------------|
|AV_ERR_REPEATED_OPERATION  |1001   |重复操作   |"已经在进行某种操作，再次去做同样的操作，则会产生这个错误。操作类别主要有：AVContext 类、房间类、设备类、成员类。AVContext 类型的操作：StartContext/StopContext。房间类型的操作：EnterRoom/ExitRoom。设备类型的操作：打开/关闭某个设备。成员类型的操作：请求画面/取消画面。"|等待上一个操作完成后再进行下一个操作。|
|AV_ERR_EXCLUSIVE_OPERATION |1002   |互斥操作   |已经在进行某种操作，再次去做同类型的其他操作，则会产生这个错误。   |等待上一个操作完成后再进行下一个操作。     |
|AV_ERR_HAS_IN_THE_STATE    |1003   |重复操作   |对象已经处于某种状态，再去做使得它进入这种状态的操作时，则会产生这个错误。如已经在房间中，再去做进入房间的操作，就会产生这个错误。|由于已经处于所要状态，可以认为该操作已经成功，当作成功来处理。|
|AV_ERR_INVALID_ARGUMENT    |1004   |错误参数   |调用 SDK 接口时，传入错误的参数，则会产生这个错误。如进入房间时，传入的房间类型不等于 AVRoom::ROOM_TYPE_PAIR 或 AVRoom::ROOM_TYPE_MULTI，就会产生这个错误。|详细阅读API文档，获取每个接口的每个参数的有效取值范围，保证传入参数的正确性并进行相应的预防处理。|
|AV_ERR_TIMEOUT             |1005   |操作超时   |进行某个操作，在规定的时间内，还未返回操作结果，则会产生这个错误。多数情况下，涉及到信令传输的、且网络出问题的情况下，才容易产生这个错误。如执行进入房间操作时，30s后还没有返回进入房间操作完成的结果的话，就会产生这个错误。	|确认网络是否有问题，是否能连接到外网环境，并尝试重试。|
|AV_ERR_NOT_IMPLEMENTED     |1006   |未实现     |调用 SDK 接口时，如果相应的功能还未支持，则会产生这个错误。|暂不支持该功能，找其他替代方案。|
|AV_ERR_NOT_IN_MAIN_THREAD  |1007   |不在主线程 |SDK 对外接口要求在主线程执行，如果业务侧调用 SDK 接口时，没有在主线程调用，则会产生这个错误。  |修改业务侧逻辑，确保在主线程调用SDK接口。|
|AV_ERR_RESOURCE_IS_OCCUPIED|1008   |资源被占用 |当需要用到某种资源，如摄像头、屏幕等，而这些资源已经被占用了，则会产生这个错误。|确认具体要用到哪些资源，及这样资源为什么被占用了，确保在正确的时机使用 SDK 相关功能以保证资源使用不冲突。 |
|AV_ERR_CONTEXT_NOT_EXIST   |1101   |AVContext 状态问题 |当 AVContext 对象未处于 CONTEXT_STATE_STARTED 状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。   |修改业务侧逻辑，确保调用SDK接口的时机的正确性。|
|AV_ERR_CONTEXT_NOT_STOPPED |1102   |AVContext 状态问题 |当 AVContext 对象未处于 CONTEXT_STATE_STOPPED 状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。如不在这种状态下，去调用 AVContext::DestroyContext 时，就会产生这个错误。|修改业务侧逻辑，确保调用 SDK 接口的时机的正确性。|
|AV_ERR_ROOM_NOT_EXIST      |1201   |AVRoom 状态问题    |当 AVRoom 对象未处于 ROOM_STATE_ENTERED 状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。|修改业务侧逻辑，确保调用SDK接口的时机的正确性。 |
|AV_ERR_ROOM_NOT_EXITED     |1202   |AVRoom 状态问题    |当 AVRoom 对象未处于 ROOM_STATE_EXITED 状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。如不在这种状态下，去调用 AVContext::StopContext 时，就会产生这个错误。    |修改业务侧逻辑，确保调用 SDK 接口的时机的正确性。  |
|AV_ERR_DEVICE_NOT_EXIST    |1301   |设备不存在 |当设备不存在或者设备初始化未完成时，去使用设备，则会产生这个错误。 |确认设备是否真的存在，确保设备 ID 填写的正确性，确保在设备初始化成功后再去使用设备。   |
|AV_ERR_ENDPOINT_NOT_EXIST  |1401|AVEndpoint 对象不存在 |当成员没有在发语音或视频文件时，去获取它的 AVEndpoint 对象时，就可能产生这个错误。 |修改业务侧逻辑，确保调用SDK接口的时机的正确性。    |
|AV_ERR_ENDPOINT_HAS_NOT_VIDEO  |1402|成员没有发视频    |当成员没有在发视频时，去做需要成员发视频的相关操作时，就可能产生这个错误。如当某个成员没有发送视频时，去请求他的画面，就会产生这个错误。   |修改业务侧逻辑，确保调用 SDK 接口的时机的正确性。  |
|AV_ERR_TINYID_TO_OPENID_FAILED |1501|tinyid转identifier失败    |当收到某个成员信息更新的信令时，需要去把 tinyid 转成 identifier，如果 IMSDK 库相关逻辑存在问题、网络存在问题等，则会产生这个错误。 |确认网络是否存在问题，查看日志确认 IMSDK 相关逻辑是否存在问题。    |
|AV_ERR_OPENID_TO_TINYID_FAILED |1502|identifier 转 tinyid 失败 |当调用StartContext 接口时，需要去把 identifier 转成 tinyid，如果 IMSDK 库相关逻辑存在问题、网络存在问题、没有处于登录态时等，则会产生这个错误。    |确认网络是否存在问题，查看日志确认 IMSDK 相关逻辑是否存在问题，确认已经成功调用 IMSDK 的登录接口。 |
|AV_ERR_DEVICE_TEST_NOT_EXIST   |1601|AVDeviceTest 状态问题 |当 AVDeviceTest 对象未处于 DEVICE_TEST_STATE_STARTED 状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。    |修改业务侧逻辑，确保调用 SDK 接口的时机的正确性。  |
|AV_ERR_DEVICE_TEST_NOT_STOPPED	|1602|AVDeviceTest 状态问题 |当 AVDeviceTest 对象未处于 DEVICE_TEST_STATE_STOPPED 状态，去调用需要处于这个状态才允许调用的接口时，则会产生这个错误。如不在这种状态下，去调用 AVContext::StopContext 时，就会产生这个错误。  |修改业务侧逻辑，确保调用 SDK 接口的时机的正确性。  |
|AV_ERR_INVITE_FAILED       |1801|发送邀请失败  |发送邀请时产生的失败。 |邀请模块只是用于 DEMO 演示方便用，对外暂不支持邀请功能，所以业务侧不需要处理这些错误码。   |
|AV_ERR_ACCEPT_FAILED       |1802|接受邀请失败  |接受邀请时产生的失败。 |邀请模块只是用于 DEMO 演示方便用，对外暂不支持邀请功能，所以业务侧不需要处理这些错误码。   |
|AV_ERR_REFUSE_FAILED       |1803|拒绝邀请失败  |拒绝邀请时产生的失败。 |邀请模块只是用于 DEMO 演示方便用，对外暂不支持邀请功能，所以业务侧不需要处理这些错误码。   |
|QAV_ERR_NOT_TRY_NEW_ROOM   |2001|没有尝试进入新房间，将停留在旧房间。  |切换到新房间失败，但仍然在当前房间 |在当前房间仍可以正常使用。 |
|QAV_ERR_TRY_NEW_ROOM_FAILED    |2002|尝试进入新房间，但失败了，旧房间也将关闭。    |切换到新房间失败，同时已退出原来的房间 |退出房间，重新进入。   |


## 服务端错误

|错误码名称                         |错误码值 |含义 |原因                                                                                          |建议方案   |
|-----------------------------------|-----|-----|----------------------------------------------------------------------------------------------|---------------------------------------------------------|
|AV_ERR_SERVER_FAILED           |10001  |一般错误   |具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 |查看并确认进房 API 中的参数，如 Appid， UIN， AuthBuffer 的合法性（参照文档）。请查看控制台上的相关参数是否与本地的一致。请查看控制台是否欠费。检查开发者测试设备网络环境，是在开发者内网环境还是外网环境。|
|AV_ERR_SERVER_INVALID_ARGUMENT |10002  |错误参数   |调用 SDK 接口时，或 SDK 内部发送信令给后台时，传了错误的参数。   |确保调用 SDK 接口时所传的参数的正确性。分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。    |
|AV_ERR_SERVER_NO_PERMISSION    |10003  |没有权限   |没有权限使用某个功能。如进入房间时所带的签名错误或过期，就会产生这个错误。   |确保在设置正确的权限参数后才去使用相应的功能。检查 appid 及权限密钥是否正确。|
|AV_ERR_SERVER_TIMEOUT          |10004  |超时      |进行某个操作，在规定的时间内，还未返回操作结果，则会产生这个错误。 |分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。   |
|AV_ERR_SERVER_ALLOC_RESOURCE_FAILED    |10005|网络错误 |执行某些操作时，网络错误   |看并确认进房 API 中的参数，如 Appid， UIN， AuthBuffer 的合法性（参照文档）。如果合法，检查开发者测试设备网络环境，是在开发者内网环境还是外网环境。如果是开发者内网，请开发者探测下 url：openmsf.3g.qq.com:15000 是否能够连接上。如上 url 成功连接，请探测下 url：cloud.tim.qq.com:15000 是否能够连通。|
|AV_ERR_SERVER_ID_NOT_IN_ROOM   |10006  |不在房间内 |在不在房间内时，去执行某些操作，则会产生这个错误。  |确保在正确的时机使用 SDK 相关功能|
|AV_ERR_SERVER_NOT_IMPLEMENT    |10007  |未实现     |调用 SDK 接口时，如果相应的功能还未支持，则会产生这个错误。    |暂不支持该功能，找其他替代方案。   |
|AV_ERR_SERVER_REPEATED_OPERATION  		|10008|重复操作 |已经在进行某种操作，再次去做同类型的其他操作，则会产生这个错误。 |等待上一个操作完成后再进行下一个操作。   |
|AV_ERR_SERVER_ROOM_NOT_EXIST   |10009  |房间不存在	|房间不存在时，去执行某些操作，则会产生这个错误。   |确保在正确的时机使用 SDK 相关功能|
|AV_ERR_SERVER_ENDPOINT_NOT_EXIST       |10010|成员不存在	|某个成员不存在时，去执行该成员相关的操作，则会产生这个错误。   |分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。   |
|AV_ERR_SERVER_INVALID_ABILITY  |10011  |错误能力   |具体原因需要通过分析日志确认后台返回给客户端的真正错误码才能知道。 |分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。   |

## 离线语音错误

|错误码名称 |错误码值 |含义  |原因  |建议方案        |
|------|-----|-----|------|------|
|QAVPTTERROR_RECORDER_PARAM_NULL                |4097   |录音错误       |参数为空|检查代码中接口参数是否正确|
|QAVPTTERROR_RECORDER_INIT_ERROR                |4098   |录音错误       |初始化错误|检查设备是否被占用，或者权限是否正常，是否初始化正常|
|QAVPTTERROR_RECORDER_RECORDING_ERR             |4099   |录音错误       |正在录制中|确保在正确的时机使用 SDK 录制功能|
|QAVPTTERROR_RECORDER_NODATA_ERR                |4100   |录音错误       |没有采集到音频数据|检查麦克风设备是否正常|
|QAVPTTERROR_RECORDER_OPENFILE_ERR              |4101   |录音错误       |录音时，录制文件访问错误|确保文件存在，文件路径的合法性|
|QAVPTTERROR_RECORDER_PERMISSION_MIC_ERR        |4102   |录音错误       |麦克风未授权错误|使用 SDK 需要麦克风权限，添加权限请参考对应引擎或平台的 SDK 工程配置文档|
|QAVPTTERROR_RECORDER_AUDIO_TOO_SHORT           |4103   |录音错误       |录音时间太短错误|首先，限制录音时长的单位为毫秒，检查参数是否正确；其次，录音时长要1000毫秒以上才能成功录制|
|QAVPTTERROR_RECORDER_RECORD_NOT_START          |4104   |录音错误       |没有启动录音操作|检查是否已经调用启动录音接口|
|QAVPTTERROR_UPLOAD_FILE_ACCESSERROR            |8193   |上传错误       |上传文件时，文件访问错误|确保文件存在，文件路径的合法性|
|QAVPTTERROR_UPLOAD_SIGN_CHECK_FAIL             |8194   |上传错误       |签名校验失败错误|检查鉴权密钥是否正确，检查是否有初始化离线语音|
|QAVPTTERROR_UPLOAD_COS_INTERNAL_FAIL           |8195   |上传错误       |网络错误|检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_UPLOAD_GET_TOKEN_NETWORK_FAIL		|8196   |上传错误       |获取上传参数过程中网络失败|检查鉴权是否正确，检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_UPLOAD_SYSTEM_INNER_ERROR          |8197   |上传错误       |获取上传参数过程中回包数据为空|检查鉴权是否正确，检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_UPLOAD_RSP_DATA_DECODE_FAIL        |8198   |上传错误       |获取上传参数过程中回包解包失败|检查鉴权是否正确，检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_UPLOAD_APPINFO_UNSET               |8200   |上传错误       |没有设置 appinfo|检查 apply 接口是否有调用，或者入参是否为空|
|QAVPTTERROR_DOWNLOAD_FILE_ACCESSERROR          |12289  |下载错误       |下载文件时，文件访问错误    |检查文件路径是否合法|
|QAVPTTERROR_DOWNLOAD_SIGN_CHECK_FAIL           |12290  |下载错误       |签名校验失败    |检查鉴权密钥是否正确，检查是否有初始化离线语音|
|QAVPTTERROR_DOWNLOAD_COS_INTERNAL_FAIL         |12291  |下载错误       |网络错误    |服务器获取语音文件失败，检查接口参数 fileid 是否正确，检查网络是否正常|
|QAVPTTERROR_DOWNLOAD_REMOTEFILE_ACCESSERROR    |12292  |下载错误       |服务器文件系统错误    |检查设备网络是否可以正常访问外网环境，检查服务器上是否有此文件|
|QAVPTTERROR_DOWNLOAD_GET_SIGN_NETWORK_FAIL     |12293  |下载错误       |获取下载参数过程中，HTTP 网络失败|检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_DOWNLOAD_SYSTEM_INNER_ERROR        |12294  |下载错误       |获取下载参数过程中，回包数据为空 |检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_DOWNLOAD_GET_SIGN_RSP_DATA_DECODE_FAIL    |12295  |下载错误       |获取下载参数过程中，回包解包失败|检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_DOWNLOAD_APPINFO_UNSET				|12297  |下载错误       |没有设置 appinfo|检查鉴权密钥是否正确，检查是否有初始化离线语音|
|QAVPTTERROR_PLAYER_INIT_ERR                    |20481  |播放错误       |初始化错误|检查设备是否被占用，或者权限是否正常，是否初始化正常|
|QAVPTTERROR_PLAYER_PLAYING_ERR                 |20482  |播放错误       |正在播放中，试图打断并播放下一个失败了（正常是可以打断的）|检查代码逻辑是否正确|
|QAVPTTERROR_PLAYER_PARAM_NULL                  |20483  |播放错误       |参数为空|检查代码中接口参数是否正确|
|QAVPTTERROR_PLAYER_OPENFILE_ERR                |20484  |播放错误       |播放时，文件访问错误|确保文件存在，文件路径的合法性|
|QAVPTTERROR_PLAYER_PLAYER_NOT_START_ERR        |20485  |播放错误       |播放未开始|确保文件存在，文件路径的合法性|
|QAVPTTERROR_S2T_INTERNAL_ERROR                 |32769  |语音转文字错误 |内部错误|分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。|
|QAVPTTERROR_S2T_NETWORK_FAIL                   |32770  |语音转文字错误 |网络失败|检查设备网络是否可以正常访问外网环境|
|QAVPTTERROR_S2T_RSP_DATA_DECODE_FAIL           |32772  |语音转文字错误 |回包解包失败|分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。|
|QAVPTTERROR_S2T_APPINFO_UNSET                  |32774  |语音转文字错误 |没有设置 appinfo|检查鉴权密钥是否正确，检查是否有初始化离线语音|
|QAVPTTERROR_STREAMIN_RECORD_SUC_REC_FAIL       |32775  |流式语音转文本错误     |流式语音转文本失败，但是录音成功了|检查网络是否正确连接，检查权限密钥是否正确|
|QAVPTTERROR_S2T_SIGN_CHECK_FAIL                |32776  |authbuffer校验失败   |authbuffer 校验失败|检查 authbuffer 是否正确|
|QAVPTTERROR_STREAMIN_UPLOADANDRECORD_SUC_REC_FAIL    |32777  |流式语音转文本错误     |流式语音转文本失败，但是录音成功了，上传也成功了。|检查代码是否有错误|
|QAVPTTERROR_S2T_PARAM_NULL                     |32784  |语音转文字错误     |语音转文本参数错误|检查代码中接口参数 fileid 是否为空|
|QAVPTTERROR_S2T_AUTO_SPEECH_REC_ERROR          |32785  |语音转文字错误     |语音转文本翻译返回错误|离线语音后台错误，请分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决|
|QAVPTTERROR_ERR_VOICE_STREAMIN_RUNING_ERROR    |32786  |流式语音转文本错误     |流式语音转文本失败|在流式录制状态当中，请等待流式录制接口执行结果返回|
