---
nav_title: フィールドレベル暗号化
article_title: フィールドレベル暗号化
permalink: "/field_level_encryption/"
description: "このリファレンス記事では、Brazeで共有される個人を特定できる情報（PII）を最小限に抑えるために、メールアドレスを暗号化する方法について説明します。"
page_type: reference
---

# フィールドレベル暗号化

> フィールドレベルの暗号化を使用すると、AWS Key Management Service (KMS) でメールアドレスをシームレスに暗号化し、Braze で共有される個人を特定できる情報 (PII) を最小限に抑えることができます。暗号化は機密データを暗号文に置き換えます。これは読み取れない暗号化された情報です。


フィールドレベルの暗号化は現在ベータ機能として利用可能です。このベータ版に参加することに興味がある場合は、Brazeのアカウントマネージャーに連絡してください。
{% endalert %}

## その仕組み

メールアドレスは、Brazeに追加される前にハッシュ化および暗号化される必要があります。メッセージが送信されると、復号化されたメールアドレスのためにAWS KMSに呼び出しが行われます。次に、ハッシュ化されたメールアドレスが配信およびエンゲージメントイベントのメタデータに挿入され、元のユーザーにリンクされます。これがBrazeがメール分析を追跡する方法です。Brazeは含まれているプレーンテキストのメールアドレスを編集し、ユーザーのプレーンテキストのメールアドレスを保存しません。

## 前提条件

フィールドレベルの暗号化を使用するには、メールアドレスをBrazeに送信する前にAWS KMSにアクセスして[暗号化](https://docs.aws.amazon.com/kms/latest/APIReference/API_Encrypt.html)および[ハッシュ化](https://docs.aws.amazon.com/kms/latest/APIReference/API_GenerateMac.html)する必要があります。 

次の手順に従って、AWSシークレットキー認証方法を設定します。

1. アクセスキーIDとシークレットアクセスキーを取得するには、AWSでIAMユーザーと管理者グループを作成し、AWS Key Management Serviceの権限ポリシーを設定します。IAMユーザーは[kms:Decrypt](https://docs.aws.amazon.com/kms/latest/APIReference/API_Decrypt.html)および[kms:GenerateMac](https://docs.aws.amazon.com/kms/latest/APIReference/API_GenerateMac.html)の権限を持っている必要があります。詳細については、[AWS KMS の権限](https://docs.aws.amazon.com/kms/latest/developerguide/kms-api-permissions-reference.html)を参照してください。
2. **ユーザーのセキュリティ認証情報を表示**を選択して、アクセスキーIDとシークレットアクセスキーを表示します。これらの認証情報をどこかにメモするか、**認証情報をダウンロード**ボタンを選択してください。AWS KMSキーに接続する際にこれらを入力する必要があります。
3. 次のAWSリージョンでKMSを設定する必要があります:
    - **Braze US クラスター:** `us-east-1`
    - **Braze EU クラスター:** `eu-central-1`
4. AWS Key Management Serviceで2つのキーを作成し、IAMユーザーがキー使用権限に追加されていることを確認します。
    - **[暗号化/復号化](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk):****対称**キータイプを選択し、**暗号化と復号化**キー使用法を選択します。
    - **[ハッシュ](https://docs.aws.amazon.com/kms/latest/developerguide/hmac-create-key.html):**対称鍵タイプを選択し、MACの生成と検証の鍵使用を選択します。キー仕様は**HMAC_256**であるべきです。キーを作成した後、HMACキーIDをどこかにメモしておいてください。Brazeに入力する必要があります。

![]({% image_buster /assets/img/field_level_encryption_aws_prereq.png %})

## ステップ 1:AWS KMS キーを接続する

AWS KMS設定には、次の内容を入力してください:

- アクセスキーID
- シークレットアクセスキー
- HMACキーID（保存後に更新することはできません）

## ステップ2:暗号化フィールドを選択してください

次に、**メールアドレス**を選択してフィールドを暗号化します。 

フィールドの暗号化が有効になっている場合、暗号化されていないフィールドに戻すことはできません。これは暗号化が永久的な設定であることを意味します。メールアドレスの暗号化を設定する際、ワークスペースにメールアドレスを持つユーザーがいないことを確認してください。これにより、ワークスペースの機能を有効にするときに、プレーンテキストのメールアドレスがBrazeに保存されないようにします。

![]({% image_buster /assets/img/field_level_encryption.png %})

## ステップ 3:インポートしてユーザーを更新する

フィールドレベルの暗号化が有効になっている場合、メールアドレスをハッシュ化して暗号化し、Brazeに追加する必要があります。ハッシュ化する前にメールアドレスを小文字にしてください。詳細については、[ユーザー属性オブジェクト](#user-attributes-object)を参照してください。

Brazeでメールアドレスを更新する際は、`email`が含まれている場所にはハッシュ化されたメールの値を使用する必要があります。これには以下が含まれます:

- RESTエンドポイント:
    - 
    - 
    - 
    - 
- CSVを介してユーザーを追加または更新する


新しいユーザーを作成する際には、ユーザーの暗号化されたメールの値を`email_encrypted`に追加する必要があります。それ以外の場合、ユーザーは作成されません。同様に、メールアドレスを持っていない既存のユーザーにメールアドレスを追加する場合は、`email_encrypted`を追加する必要があります。それ以外の場合、ユーザーは更新されません。


## 考慮事項

これらの機能はフィールドレベルの暗号化ではサポートされていません:

- SDKを介してメールアドレスを識別およびキャプチャする
- アプリ内メッセージメールキャプチャフォーム
- 受信者ドメインに関するレポート、メールインサイトのメールボックスプロバイダーチャートを含む
- メールアドレスフィルター正規表現による
- オーディエンス同期
- Shopify統合

### ユーザー属性オブジェクト

`/users/track` エンドポイントでフィールドレベルの暗号化を使用する場合、[ユーザー属性オブジェクト]({{site.baseurl}}/api/objects_filters/user_attributes_object)のフィールドの詳細に注意してください:

- `email`フィールドはメールのハッシュ値でなければなりません。
- `email_encrypted`フィールドはメールの暗号化された値でなければなりません。

## よくある質問

### 暗号化とハッシュ化の違いは何ですか？

暗号化は、データを暗号化および復号化することが可能な双方向機能です。同じ平文の値が複数回暗号化された場合、AWSの暗号化アルゴリズム（AES-256-GCM）は異なる暗号化値を生成します。ハッシュ化は、平文が復号できない方法でスクランブルされる一方向関数です。ハッシュ化は毎回同じ値を生成します。これにより、同じメールアドレスを共有する複数のユーザー間でサブスクリプション状態を維持することができます。

### テスト送信にどのメールアドレスを使用すればよいですか？
プレーンテキストのメールアドレスはテスト送信でサポートされています。特定のユーザーに対してメールがどのように見えるかを確認するには、次の手順を実行します。

1. **プレビュー メッセージをユーザーとして選択**.
2. **テスト送信**で、**現在のプレビューユーザーの属性で受信者の属性を上書き<2>}を選択します。


### このメールアドレス Liquid `{{${email_address}}}` を Braze に追加するとどうなりますか？

Brazeはメールを送信する際にプレーンテキストのメールアドレスをレンダリングします。プレビューでは、メールの暗号化されたバージョンを表示します。カスタムワンクリックURLでユーザーを参照する場合は、ユーザーのexternal IDを使用することをお勧めします。

`{{${email_address}}}`は現在、ユーザー設定センターおよび配信停止ページではサポートされていません。
{%endraw%}

### Currentsで確認するメールアドレスは何ですか？

ハッシュ化されたメールアドレスは、メール配信およびエンゲージメントイベントに含まれています。

### メッセージアーカイブでどのメールアドレスを確認すればよいですか？

プレーンテキストのメールアドレスはメッセージングアーカイブに含まれています。これらは顧客のクラウドストレージプロバイダーに直接送信され、メール本文に他の個人データが含まれている場合があります。

### サブスクリプション管理にフィールドレベルの暗号化を使用して、メールリストの配信停止を行うことはできますか？

いいえ。メール-toリスト-配信停止を使用すると、平文の復号化されたメールアドレスがBrazeに送信されます。フィールドレベルの暗号化が有効になっている場合、URLベースのHTTP:メソッドをサポートしており、ワンクリックも含まれます。また、メール本文にワンクリックで配信停止できるリンクを含めることをお勧めします。