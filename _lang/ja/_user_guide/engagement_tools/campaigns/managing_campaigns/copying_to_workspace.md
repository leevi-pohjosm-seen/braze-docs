---
nav_title: ワークスペース間でのコピー
article_title: ワークスペース間でのコピー
alias: "/copying_to_workspaces/"
page_order: 0.5
page_type: reference
description: "この記事では、ワークスペース間でキャンペーンをコピーする方法の概要を説明します。"
tool: Campaigns
---

# ワークスペース間でキャンペーンをコピーする

> ワークスペース間でキャンペーンをコピーすると、別のワークスペースにあるキャンペーンのコピーを利用して、メッセージの作成をすぐに開始できます。このコピーは、編集して開始するまで下書きとして残り、成功したメッセージング戦略を維持し、構築するのに役立ちます。

{% alert important %}
ワークスペース間でのキャンペーンのコピーは、一般に以下のサポートされているチャネルで利用できます: SMS、アプリ内メッセージ、メール、メールテンプレート、およびコンテンツブロック。他のチャネルのサポートも近日中に開始される予定です。
{% endalert %}

## キャンペーンをコピーする方法

![][1]{: style="float:right;max-width:70%;margin-left:15px;"}

キャンペーンをワークスペース全体にコピーするには、選択したキャンペーンの横にある歯車アイコン <i class="fas fa-cog"></i> をクリックし、[**ワークスペースにコピー**] をクリックします。コピー後、キャンペーンをレビューおよびテストして、すべてのフィールドが適切に機能していることを確認するようお勧めします。

キャンペーンをワークスペースにコピーすると、キャンペーンの名前と説明、バリアント、配信スケジュールのタイプ、コンバージョン行動などのフィールドがコピーされます。メールキャンペーンの場合、メールの本文、件名、プリヘッダーなどのフィールドも、コピー先のワークスペースにコピーされます。 

サポートされていないチャネルを含むマルチチャネルキャンペーンはワークスペースにコピーできないことに注意してください。

### Liquid を含むキャンペーンのコピー

Liquid 参照を含むメッセージ本文の場合、参照はワークスペースにコピーされますが、期待どおりに機能しない可能性があります。これは、ワークスペース A のキャンペーンがワークスペース B にコピーされた場合、ワークスペース B は、Liquid 参照を含むワークスペース A の詳細を参照できないことを意味します。たとえば、トリガーアクションやオーディエンスフィルターなどのフィールドは、ワークスペース間でコピーされません。

ワークスペース間でキャンペーンをコピーする場合は、依存関係のある以下の Liquid 参照に注意してください。
\- カタログアイテムタグ
\- コネクテッドコンテンツタグ
\- コンテンツブロック
\- カスタム属性
\- ユーザー設定センター
\- おすすめ商品
\- サブスクリプションの状態タグ
\- クーポンとプロモーションタグ

ワークスペース内でキャンペーンをコピーする場合、コンテンツブロックはコピーされません。ただし、同じ名前のブロックが存在する場合、宛先のワークスペースでコンテンツブロックを参照できます。あるいは、宛先のワークスペースにコンテンツブロック (またはこれらの Liquid 参照) を作成して、キャンペーン開​​始時のエラーを回避することもできます。

### ワークスペース間でコピーされる内容

以下は、ワークスペース内でコピーされる内容と省略される内容の包括的なリストではないことに注意してください。ベストプラクティスとして、キャンペーンの詳細を確認し、キャンペーンが期待どおりに機能することをテストしてください。

{% tabs %}
{% tab キャンペーン %}

| コピーされる内容 | 省略される内容 |
|---|---|
| 説明 | 地域 |
| タイプ | タグ |
| アクション (ネスト) | セグメント |
| コンバージョン行動 (ネスト) | 承認 |
| サイレント時間の設定 | トリガースケジュール |
| フリークエンシーキャップの設定 | キャンペーン概要 |
| 受信者のサブスクリプション状態 |  |
| 定期的なスケジュール |  |
| トランザクションである |  | 

{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab コンバージョン行動 %}

| コピーされる内容 | 省略される内容 |
|---|---|
| タイプ行動 | ワークスペース ID |
| キャンペーンのインタラクション |  キャンペーン ID |
| カスタムイベント名 |  |
| 製品名 |  |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab アクション %}

| コピーされる内容 | 省略される内容 |
|---|---|
| アクションのタイプ | 送信カウント |
| メッセージのバリエーション |  |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab メッセージのバリエーション %}

| コピーされる内容 | 省略される内容 |
|---|---|
| 送信割合 | API ID |
| タイプ |  シードグループ ID |
|  |  リンクテンプレート ID |
|  |  内部ユーザーグループ ID |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab メールメッセージのバリエーション %}

| コピーされる内容 | 省略される内容 |
|---|---|
| [メール本文]({{site.baseurl}}/user_guide/engagement_tools/campaigns/managing_campaigns/copying_to_workspace/?tab=email%20body) | 差出人アドレス |
| メッセージエクストラ |  返信先 |
| タイトル |  BCC |
| 件名 |  リンクテンプレート |
|  |  リンクエイリアス |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab メール本文 %}

| コピーされる内容 | 省略される内容 |
|---|---|
| プレーンテキスト | リンクエイリアス |
| HTML とドラッグ＆ドロップコンテンツ |  |
| プリヘッダー |  |
| インライン CSS |  |
| AMP HTML |  |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab メールテンプレート %}

| コピーされる内容 | 省略される内容 |
|---|---|
| [メール本文]({{site.baseurl}}/user_guide/engagement_tools/campaigns/managing_campaigns/copying_to_workspace/?tab=email%20body) | API ID |
| 説明 | 画像 ID |
| 件名 | 地域 |
| ヘッダー | タグ |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab コンテンツブロック %}

| コピーされる内容 | 省略される内容 |
|---|---|
| 名前 | リンクエイリアス |
| 説明 | API キー |
| コンテンツ | 地域 |
| HTML とドラッグ＆ドロップコンテンツ | タグ |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% tab SMS メッセージのバリエーション %}

| コピーされる内容 | 省略される内容 |
|---|---|
| 本文 | メッセージングサービス |
| リンク短縮 | VCF メディアアイテム |
| クリック追跡 |  |
| メディアアイテム |  |
{: .reset-td-br-1 .reset-td-br-2}

{% endtab %}
{% endtabs %}

[1]: {% image_buster /assets/img_archive/clone_campaign.png %}
