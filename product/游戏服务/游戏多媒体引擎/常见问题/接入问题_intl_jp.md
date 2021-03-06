## 概要

Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここではSDKでよくある質問と解答を紹介します。以下はいくつかのよくある技術的な質問と解答、そして一般的なコンセプトの理解です。本ドキュメントは今後も引き続き補足されます。

## 一般的な質問

### ゲームマルチメディアエンジン（GME）には、どのような具体的な機能がありますか？

ゲームマルチメディアエンジン（GME）は、リアルタイムボイス、オフラインボイスメッセージ及びボイスのテキスト認識機能をサポートします。

### ゲームマルチメディアエンジン（GME）が対応可能なゲームシナリオにはどのようなものがありますか？

eスポーツ、国戦ゲーム、カジュアルゲーム、人狼ゲーム等があります。

### GMEはどのゲームエンジン及びプラットフォームをサポートしていますか？

GMEが現在サポートしているゲームエンジンにはUnity、Unreal及びCocos2dがあります。サポートしているプラットフォームにはWindows、Mac、iOS及びAndroidがあります。

### どのようにしてGMEの使用を開始しますか？

Tencent Cloudゲームマルチメディアエンジン（GME）を効果的に使用するために、ゲーム用音声ビデオエンジンの初期導入を案内する[導入ガイドドキュメント](https://cloud.tencent.com/document/product/607/10782)を用意しました。

### Androidのsoライブラリにarmv8はありますか？

現在はサポートしていませんが、後続のバージョンにてサポートする予定です。

### 認証の安全性はどのように保証されていますか？

一般的な推奨事項として、導入初期段階でクライアント配置案を使用することを推奨します。後でゲームAppのバックグラウンドに配置するよう最適化することができます。

| 解決策       | 強み     | 弱み             |
| ---------- | -------- | ---------------- |
| バックグラウンド配置   | 安全性が高い | バックグラウンド開発との共同デバッグが必要 |
| クライアント配置 | 導入が迅速 | 安全性が低い         |


### リアルタイムボイス及びオフラインボイス導入過程で、認証失敗を示すエラーコードが出ました。どのように処理すればよいですか？
リアルタイムボイス及びオフラインボイス導入過程で認証エラーが出た場合、まずコンソールでオフラインボイスサービスが有効であるかを確認してください。有効な場合は、以下の事項を確認してください。
1、sdkappidがコンソールと一致しているか。
2、OpenIDは10000より大きくする必要があります。
3、オフラインボイスのルーム番号パラメータは、0にする必要があります。
4、Tencent Cloudコンソールから送られる暗号鍵が一致しているか。

## 公式サイトからのダウンロード及びDemoの変更に関連する質問

### ゲームマルチメディアエンジン（GME）Demo及びSDKはどこでダウンロードできますか？

[ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連するDemo及びSDKをダウンロードしてください。現在、公式サイトにはUnityエンジンDemo、Cocos2DエンジンDemo、Androidネイティブ開発Demo及びiOSネイティブ開発Demoがあります。

### ゲームマルチメディアエンジン（GME）Demoをダウンロード後、自分が申請したアカウントに変更することはできますか？

1、できます。コンソールでsdkappidと権限暗号鍵の2つの番号を取得する必要があります。
2、オフラインボイスを使用する必要がある場合、更にTLS署名暗号鍵を取得する必要があります。以上の番号の具体的な取得方法は[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。
3、リアルタイムボイスが自身のappidを使用する場合、AVChatViewController中のGetAuthBufferでリアルタイムボイスのkeyを変更する必要があります。

### Demoを使用する時、エラーメッセージerrinfo=priv map info errorが出ました。

関連するルーム参加パラメータにエラーが発生した場合、sdkappid、権限暗号鍵が置き換えられていないか確認してください。



## 課金問題

### GMEのリアルタイムボイスサービスの課金モードには、どのようなものがありますか？どのように選択しますか？

リアルタイムボイスサービスは、ボイスDAUに応じた課金とボイス使用時間に応じた課金の2種類の課金モードをサポートしています。課金モードを選択後は変更することができません。詳細な価格は、[製品価格ドキュメント](https://cloud.tencent.com/document/product/607/17808) で確認することができます。
ボイスDAUに応じた課金を選択した場合、ボイス時間が制限され90分を越えることができず、時間制限を越えるとシステムにより自動的にルームが解散されます。対戦型、カジュアル型ゲームは、ボイスDAUに応じた課金を選択することをお勧めします。
ボイス時間に応じた課金を選択した場合、ボイス時間に制限がありません。SNS、VJ、コミュニケーション類のアプリはボイス時間に応じた課金を選択することをお勧めします。

### ボイスDAUに応じた課金を選択した場合、90分を越えるとルームはどうなりますか？

この課金モードでは、90分を越えるとルームが自動的に解散されます。解散される時にコールバック関数が届きます。

### GMEのリアルタイムボイスサービスのDAUは、どのように計算しますか？

アプリ内のユーザーがルームに参加するとボイスDAUとしてカウントされ、ボイスDAUがUserId別に計算されます（UserIdはアプリ内ユーザーの一意の識別子であり、1人のユーザーに1つのUserIdが割り当てられます）。

### GMEのリアルタイムボイスサービスのボイス時間は、どのように計算しますか？

アプリ内のユーザーがルームに参加すると、ボイス時間とカウントされます。

### GMEのボイスメッセージ及びテキスト変換サービスの課金モードには、どのようなものがありますか？どのように選択しますか？

ボイスメッセージ及びテキスト変換サービスは、ボイスメッセージDAUに応じて課金されます。詳細な価格は、[製品価格ドキュメント](https://cloud.tencent.com/document/product/607/17808)で確認することができます。

## GMEのボイスメッセージ及びテキスト変換サービスDAUは、どのように計算しますか？

アプリ内のユーザーがボイスメッセージを送信するとボイスメッセージDAUとしてカウントされ、ボイスメッセージDAUがUserId別に計算されます（UserIdはアプリ内ユーザーの一意の識別子であり、1人のユーザーに1つのUserIdが割り当てられます）。



## リアルタイムボイスサービスによくある質問

## リアルタイムボイスサービスは、どのようなゲームシナリオをサポートしますか？

およそ以下の3種類のシナリオがあります。
**マイク交互使用モード：**ユーザーが交互にマイクを使用するモードで、音質が非常に滑らかなため、人狼ゲーム等のシナリオでのボイスに適します。
**自由通話モード：**複数の人による同時通話をサポートするモードで、超低遅延のため、複数の人がチームを組んでコミュニケーションを行う等の競技ゲームのシナリオに適します。
**指揮モード：**1対多の指揮戦闘や、ライブ配信パーソナリティーの音声ゲーム共同参加等のシナリオに使用され、大型国戦ゲームに適します。

### どのようにして適切なオーディオタイプを選びますか？

### 適用シナリオによって様々なオーディオタイプがあります。具体的には以下の表を参照してください。

| オーディオタイプ                   | 意味     | パラメータ | 音量タイプ                         | 推奨コンソールサンプリングレートの設定                                    | 適用シナリオ                                                     |
| -------------------------- | -------- | ---- | -------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------ |
| ITMG_ROOM_TYPE_FLUENCY     | スムーズな音質　| 1    | スピーカー：通話音量、イヤフォン：メディア音量。 | 音質に特に要望がない場合は、16Kのサンプリングレートで十分。                    | スムーズさを優先に、超低遅延リアルタイムボイスで、FPS、MOBA等のようなゲーム内のボイスシナリオに適用されます。 |
| ITMG_ROOM_TYPE_STANDARD    | 標準音質 | 2    | スピーカー：通話音量、イヤフォン：メディア音量。 | 音質に対する要望に基づき、16k/48kのサンプリングレートを選択可能。                 | 時間遅延が適当な良好音質で、人狼殺、ボードゲーム等、カジュアルゲームのリアルタイム通話シナリオに適用されます。 |
| ITMG_ROOM_TYPE_HIGHQUALITY | 高音質 | 3    | スピーカー：メディア音量、イヤフォン：通話音量。 | 最良の効果を保証するため、コンソールで48kサンプリングレートの高音質構成に設定するのをお勧めます。 | 時間遅延が大きな超高音質で、音楽やダンスのゲームおよびボイスソーシャルAPPに適用されます。音楽再生、オンラインカラオケ等、高音質シナリオに適用されます。 |

使用するシナリオに応じて、コンソールで該当するサンプリングレート（16kまたは48k）を選択してください。開発導入中にAPIよりオーディオタイプを調整できますが、サンプリングレートはコンソールで選択した値以下にする必要があります。例えば、コンソールで16kのサンプリングレートを選択した場合、クライアントで高音質に調整したとしても、サンプリングレートは16kのままです。コンソールで48kのサンプリングレートを選択し、クライアントで滑らかな音質に調整した場合、サンプリングレートは16kになります。



### イベントのトリガには周期的にpoll関数を呼び出す必要がありますが、新たにスレッドを開く場合、定刻にウェイクアップし、その後、poll関数を呼び出してもよいですか？

当社のAPIは、理論上、同一スレッド上で呼び出す必要があります。サブスレッドでの呼び出しを選択した場合も、同一サブスレッド上で呼び出すことを確保してください（特にInitとPoll）。

### poll関数の呼び出す時間間隔はどのぐらいが適切ですか？

特に要件がない場合は、Demoを参照して呼び出してください。

### GMEリアルタイムボイスのルーム数には制限がありますか？人数には制限がありますか？

リアルタイムボイスのルーム数には制限がありません。人数にも制限がありません。

### 何故、ルームに参加するときにHttp Invalid idが返されますか？

現在、API上のパラメータuseridのタイプはstringタイプですが、実際、当社内部でstringタイプをuint64タイプに強制変換します。変換ができないまたは変換後の結果が10000未満の場合、ルーム参加ができず且つHttp Invalid idが返されます。
お客様のアカウントが0から始まる場合、アカウントに10000を加えることをお勧めします。例えば、アカウントが999の場合、入力する数字は10999になります。

### ルーム番号を回収するAPIがありますか？

回収するAPIがありません。最後の1人がルームから退出すると、ルームは自動的に終了します。

### ルーム番号の値には要求がありますか？

roomidは現在32ビットの符号なし整数型しかサポートしません。

### openidの値には要求がありますか？

openidは現在64ビットの符号なし整数型しかサポートしません。stringに変換してSDKに入力してください。

### 単一openidで同時に複数のルームに参加することはできますか？

できません。1つのopenidは同時に1つのルームにしか存在できません。

### ルーム退出とルーム参加は同期しない操作ですか？この2つのAPIを同時に呼び出すことはできますか？

まずexitroomを呼び出し、ルーム退出完了のコールバックを受信してから、再度enterroomを呼び出す必要があります。

### メンバーステータスの同期のタイミングは？初めてルームに参加した時に通知されますか？

オーディオイベントの通知にはしきい値があり、このしきい値を越えると「メンバーがオーディオパケットを送信した」通知が送信されます。ルームメンバーが2秒間話さなかった場合、「メンバーがオーディオパケットの送信を停止した」通知が送信されます。初めてルームに参加する時に通知されます。

### ルームに参加する前にマイクの音量を設定できますか？

できません。ルームに参加する間にのみリアルタイムボイスに関連するAPI ITMGAudioCtrl ITMGAudioEffectCtrlを呼び出すことができます。

### マイクの権限占有に関する具体的な状況は？

EnterRoom関数の呼び出しが完了後、マイクの権限が占有されます。この間、その他のプログラムがマイクデータの収集を行うことができません。
EnableMic(false)を呼び出すことによりマイクの占有をリリースすることはできません。
確実にマイクをリリースする必要がある場合、PauseAudioを呼び出してください。PauseAudioを呼び出す後、エンジンが完全に一時停止し、ResumeAudioを呼び出すと回復することができます。

### EnableMic関数を呼び出す前にマイクの状態を取得するAPIはありますか？

getMicCount APIを利用してマイクが使用可能かどうかを確認することができます。

### プレイヤー同士が話をしている時に、他のオーディエンスが聞くことしかできないという要望はどのように解決しますか？

開発者がクライアントで関連機能を実装し、他のオーディエンスがマイクを有効にすることを禁止できます。

### 開発者はBGMが再生されているかについてどのように判断しますか？

IsAccompanyPlayEnd() APIを利用します。

### SDKを使用する時に、エミュレータにログインしても曲を流すことができず、コンピュータのサウンドカードを使うこともできません。

エミュレータはmp3をサポートしません。

### SDKは受話器による音声の再生をサポートしますか？

リアルタイムボイスは受話器による音声の再生をサポートしません。

### SDKがサポートするローカルオーディオファイルフォーマットを教えてください。
m4a、wav、mp3の全部で3種類のフォーマットです。

### GMEのリアルタイムボイスのチームボイスをどのように導入しますか？チームボイスには距離による減衰がありますか？

リアルタイムボイスチームボイスの導入は[チームボイスドキュメント](https://cloud.tencent.com/document/product/607/17972)を参照してください。チームボイス機能を有効にした後、同一チーム間のボイスには距離による減衰がなく、グローバルボイスには距離による減衰があります。減衰係数はドキュメントを参照してください。

### 3D効果音を実現するために、ユーザーが使用するマイクとスピーカーにはどのような要求がありますか？

3D効果音を実現するために、再生側はデュアルチャンネルをサポートする必要があります。

### GMEリアルタイムボイスの3D効果音をどのように導入しますか？

リアルタイムボイスの3D効果音の導入は[3D効果音ドキュメント](https://cloud.tencent.com/document/product/607/18218)を参照してください。

### ダウンロードしたSDKドキュメントとDemoにAuthbufferファイルがありません。

Authbufferファイルは既に統合されました。SDKで一斉検索してみてください。

### teaの暗号化にlibファイルはありますか？

当社では[Authbufferコンパイルドキュメント及びzipパッケージ](https://cloud.tencent.com/document/product/607/30281)を提供しています。

### ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECTがネットワークの切断により送信されました。一般的にどのような状況で送信されますか？具体的に接続がどのぐらい切断された時に送信されますか？

ネットワークが根本から切断され、ハートビートパケットがなくなって30秒後に現れます。

## ボイスメッセージ及びテキスト変換サービスによくある質問

### GMEのボイスメッセージとテキスト変換サービスはどのような音声をサポートしますか？

現在、Tencent Cloudコンソールで開設されるボイスメッセージとテキスト変換サービスは中国語のみをサポートします。他言語のテキスト変換サービスをご希望の場合、業務担当までお問い合わせください。

### GMEのボイスメッセージとテキスト変換サービスはリアルタイムボイスと一緒に使えますか？

はい、一緒に使えます。関連APIを呼び出して変換できます。

## GMEのボイスメッセージ及びテキスト変換サービスが常にOKを返しますが、機能を使用することができません。

GMEのボイスメッセージとテキスト変換サービスは、モバイル端末からエクスポートしてテストする必要があります。

### ボイスファイルをアップロードするAPIを呼び出してアップロードした後、戻り値のfileidがURLですが、これはどのように使用しますか？

ファイルをダウンロードするAPIを呼び出してから、このURLを使用してファイルをダウンロードします。

## SDKログ取得及びトラブルシューティングによくある質問

### どのようにログを取得しますか？

QAVSDK_日付.logファイルは、ログファイルです。ディレクトリは以下のとおりです。

| プラットフォーム    | パス                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

### 音声遅延の主な原因は？

1.**音楽再生遅延：**司会者が外部デバイスを使用して音楽を再生し、別の携帯電話で声音を収集し配信する場合（この場合必ず遅延が発生するため、イヤフォンを付けることをお勧め）。
2.**ネットワーク遅延：**上りリンクのパケットロス率が高すぎる、または上りリンクの遅延変動が大きい状況において、オーディエンスには遅延した音声が聞こえます。
















