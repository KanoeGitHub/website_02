---
published: true
layout: post
title: Mattermost を利用したSlackのログ取り
author: Kanoe
categories: プログラミング
tags:
- GAS
- Matrtermost
- Slack

---

# 経緯
Slackの無料プランでは、発言が1万件を超えた場合、古いものから順に見れなくなっていきます。有料プランに移行する方法もあるのですが、なるべくコストを抑えてこの問題を解決したいために、Slackによく似たOSSを利用できないかを考え、Mattermostというossにたどり着きました。しかしながら、今更SlackのチャンネルユーザーがMattermostに登録し直すのはかなりめんどくさいので、Slackの発言をMattermostに転送することでログを残せないかを考えました。

<!-- more -->

[完成イメージ]

- slack側  
![slack.png](https://qiita-image-store.s3.amazonaws.com/0/177611/59e63a9e-ee42-f3c6-060f-4859b0b54005.png)

- Mattermost側  
![mm.png](https://qiita-image-store.s3.amazonaws.com/0/177611/c60bc638-340e-e491-05bb-6765855bff20.png)

# 使用するもの
Mattermost
Slack
Google Apps Script
Google Cloud Pratform

# Mattermostの導入
参考①：https://docs.mattermost.com/install/install-rhel-71.html
参考②：https://qiita.com/hanaita0102/items/a684effed7e2cba157ae
ちなみに私が導入した時はバージョンが 4.8.0 でした。
バージョンは[こちら](https://about.mattermost.com/download/)でチェック
サーバーはGCPの無料枠を採用しました。

# 転送の方法
### 1.Mattermostで内向きのウェブフックの設定
　Mattermostのメニューの統合機能から内向きのウェブフック(Incoming WebHooks)を設定します。
　転送したいチャンネルを指定します。タイトルと説明は任意で構いません。
　ユーザー名とプロフェール画像については空欄にしておきます(Slackから反映させるため)。
　後ほどURL(一部モザイクのところ)を利用いたします。

![スクショ.png](https://qiita-image-store.s3.amazonaws.com/0/177611/c15643bf-99ab-12b1-9120-5b0331c8b95b.png)


### 2.Slackで外向きのウェブフックの設定
　Slackのメニューの Administration > Manage apps から Custom Integrations を選択します。
　今回は Outgoing WebHooks を選択します。
　Integration Settings 内の Channel を転送したいチャンネルに設定しておきます。
　後ほどToken(黒塗り)を使用します。
<br>
![100.png](https://qiita-image-store.s3.amazonaws.com/0/177611/1ecdc63e-30ab-674f-4fb2-6754be26ba8a.png)

　また、以下のURLからSlack APIのトークンも取得しておきます。
　https://api.slack.com/custom-integrations/legacy-tokens

### 3.GASにコードを記述
　以下のコードを作成しました。みんな大好きレッツコピペ。

```js:Slack2Matter

function doPost(e) {
	var t = e.parameter.token;

	//slackのwebhookトークン照合
	if( t != "[slack WebHook Token]")
	{return;}  

	 var chName = e.parameter.channel_name;
	 var userName = e.parameter.user_name;
	 
    //slackapiのためのコード
	var user_options = {
	 "method" : "post",
			"payload" : {
				"token" : "[slack API Token]",
				"user" : e.parameter.user_id,
			}
		};
	var response = UrlFetchApp.fetch("https://slack.com/api/users.info", user_options);
	var json = JSON.parse(response.getContentText());

	
	var name = json["user"]["real_name"];    //本名表示
	var image = json["user"]["profile"]["image_24"];   //発言者のslackアイコンを指定
	var msg = "チャンネル名：" + chName + "\n内容 : "+ e.parameter.text ;
	
	var payload = {
			"text" : "Slackから転送\n" + msg, //転送メッセージを設定
		    "icon_url" : image,  //アイコン画像を設定
			"username" : name, //Mattermostでの表示名を設定
		}
		
	postMmost(payload);
}

function postMmost(payload)
{
	var options = {
		"method" : "POST",
		"contentType" : "application/json",
		"payload" : JSON.stringify(payload)
	}

	var url = "[MatterMost Incoming Webhook URL]"; 
	var response = UrlFetchApp.fetch(url, options);
	var content = response.getContentText("UTF-8");

}

```

5行目の[slack WebHook Token]を先ほど発行したSlackのWebHooksのトークンに書き換えます。
15行目の[slack API Token]をSlackのAPIアクセストークンに書き換えます。
44行目の[MatterMost Incoming Webhook URL]を、先ほどのMattermostのWebHookで設定したURLに書き換えます。

### 4.実行
　ウェブアプリケーションとして実行します。

 ![スクリーンショット 2018-04-09 17.10.21.png](https://qiita-image-store.s3.amazonaws.com/0/177611/123ddf57-063d-75be-c0f7-3a637e8f60f6.png)

　すると「現在のウェブアプリケーションのURL」が出てくるのでそのURLをSlackのWebHooksの設定画面のURLの欄(赤矢印)に入力し保存します。

![スクリーンショット 2018-04-09 17.13.35.png](https://qiita-image-store.s3.amazonaws.com/0/177611/4ac66752-b336-5cfe-6235-cb22a86b737e.png)

![100.png](https://qiita-image-store.s3.amazonaws.com/0/177611/b0645127-4c29-0c29-9b68-45bc09603773.png)

### 5.設定したチャンネルで発言する

- slack側  
![slack.png](https://qiita-image-store.s3.amazonaws.com/0/177611/59e63a9e-ee42-f3c6-060f-4859b0b54005.png)
　

- Mattermost側  
![mm.png](https://qiita-image-store.s3.amazonaws.com/0/177611/c60bc638-340e-e491-05bb-6765855bff20.png)

　と、こんな感じになります。

# 課題点
- 転送するチャンネル毎に手作業で追記しなければならない
- 画像がslack内のリンクになる
- @付きの発言ではslackユーザーIDが転送される
- Slack上での発言の編集結果は転送されない

# 結論
多少問題点がありますが、これで**無料**でslackのログ取りが可能となりました。
\\(^o^)/
