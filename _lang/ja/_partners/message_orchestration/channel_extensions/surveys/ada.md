---
nav_title: Ada
article_title: Ada
description: "この参考記事では、顧客とのやり取りを自動化し、パーソナライズするAIを搭載したプラットフォームであるBrazeとAdaのパートナーシップについて概説している。この統合により、自動化されたエイダとの会話から収集したデータでユーザー・プロフィールを補強することができる。"
alias: /partners/ada/
page_type: partner
search_tag: Partner

---

# Ada

> [Adaは](https://ada.cx)、会話型AIを使って顧客体験を自動化し、パーソナライズするブランド・インタラクション・プラットフォームだ。Adaを使用して、ユーザーデータに基づいてメッセージングを調整し、キャンペーンをセグメント化し、会話を測定・分析して新たな機会を発見し、顧客とのチャットから得た洞察を使用してユーザープロファイルを充実させる。  

BrazeとAdaの統合により、自動化されたAdaの会話から収集したデータでユーザープロフィールを補強することができる。Adaチャット中に収集した情報に基づいてカスタムユーザー属性を設定し、Ada会話中の指定ポイントでBrazeにカスタムイベントを記録することができる。エイダ・チャットボットをBrazeに接続することで、消費者がブランドについてどのような質問をしているのか、あるいは消費者と積極的に会話を始めることで、消費者の興味や嗜好についてより深く知ることができる。

## 前提条件

| 必要条件 | 説明 |
| ----------- | ----------- |
| エイダアカウント | このパートナーシップを利用するには、BrazeとAnswer Utilitiesのアプリケーションを有効にした[Ada](https://ada.cx)アカウントが必要である。 |
| Braze REST API キー | `users.track` 権限を持つ Braze REST API キー。<br><br> これは、Brazeダッシュボードの**「設定」**>「**APIキー**」から作成できる。 |
| Braze RESTエンドポイント | [RESTエンドポイントのURL][1]。エンドポイントは、インスタンスのBraze URLに依存する。 |
{: .reset-td-br-1 .reset-td-br-2}

## ユースケース

BrazeとAdaの統合の一般的な使用例には次のようなものがある：
- Brazeのカスタムイベントとして、消費者とAdaボットのさまざまなやりとりを追跡する。これにより、どの顧客がAdaのプロアクティブキャンペーンに参加したのか、サポートエージェントに引き渡されたのか、特定の質問をしたのか、特定のアクションを完了したのかを知ることができる。
- 消費者に興味、嗜好、人口統計などを尋ねる。カスタム属性を使用して、この新しい情報でBrazeのプロフィールを自動的に更新する。

## 統合

BrazeとAdaを統合するには、まずAdaダッシュボードでBrazeアプリケーションを設定し、Adaチームと協力してAda埋め込みスクリプトにユーザーIDメタ変数を設定する必要がある。次に、Brazeに情報を送り返したい場所（イベントかアトリビュート）に、Brazeブロックをアンサーエディタにドラッグする。

### ステップ1:AdaでBrazeアプリをセットアップする

Adaのダッシュボードで、**Settings > Integrations > Handoff Integrationsと**進む。

Brazeの横にある「**Connect**」をクリックし、以下の情報を入力する：
- **RESTエンドポイント**：Braze RESTエンドポイントのURLを入力する。 
- **APIキー**：Braze REST APIキーを入力する。 
- **アプリID**：Adaチャッターを関連付けたいアプリIDを入力する。

### ステップ2:BrazeからAdaに識別子を渡す

正しいユーザーを更新していることを確認するには、Adaチームに連絡する必要がある。Adaチームは、Brazeから識別子を受け取るためにAdaの埋め込みスクリプトに必要な修正を加える手助けをすることができる。この統合は外部IDを受け取るように設計されているが、ユーザーエイリアスなど他の識別子を渡すことも可能だ。 

### ステップ3:ブレイズ・ブロックを該当するアンサーにドロップする。

Brazeブロックを使用するには、ブロックドロワーから適切なAnswerにドラッグし、アクションを選択する。ブレイズ・ブロックでは、2つのアクションができる：
* トラックイベント
* 属性を更新する

{% tabs ローカル %}
{% tab 走行会 %}

#### 回答 ユーティリティ・ブロック

1. ブロック・ドロワーからアンサー・ユーティリティーズ・ブロックを、ブレイズ・ブロックの真上にドラッグする。 
2. **Format Date**アクションを選択し、**Date**フィールドに`today` 。
3. **出力形式」**フィールドに「`iso` 」と入力する。**レスポンスを変数として保存**」で、`iso_time` という**書式付き日付の**変数を作成する。

![アンサー・ユーティリティ・ブロックには、前文で説明したようにフィールドが設定される。]({% image_buster /assets/img/ada/ada-braze-2.png %})

#### ブレーズ・ブロック

**4\.**Brazeブロックの**External ID**フィールドに、前のステップでAdaが設定した`external_id` メタ変数を入力する。<br>
**5\.****Event Name**フィールドに、追跡したいBrazeのイベント名を入力する。<br>
**6\.****Time of Event**フィールドに、Answer Utilitiesブロックで作成した変数`iso_time` を入力する。<br>
**7\.**Brazeへのイベント投稿中に問題が発生した場合に表示されるフォールバックアンサーを選択する。

![] （{% image_buster /assets/img/ada/ada-braze-3.png %} ）。

{% endtab %}
{% tab 更新属性 %}

#### ブレーズ・ブロック

1. Brazeブロックの**External ID**フィールドに、前のステップでAdaが設定した`external_id` メタ変数を入力する。 
2. **Attribute Name（属性名**）フィールドに、追跡したいBraze属性の名前を入力する。 
3. **属性値**フィールドに、設定したい値を入力する。テキスト、変数、またはテキストと変数の組み合わせである。 
4. Brazeへの属性の投稿中に問題が発生した場合に表示されるフォールバックアンサーを選択する。

![] （{% image_buster /assets/img/ada/ada-braze-4.png %} ）。

{% endtab %}
{% endtabs %}

[1]: {{site.baseurl}}/developer_guide/rest_api/basics/#endpoints
[2]: {% image_buster /assets/img/ada/ada-braze-1.png %}
[3]: {% image_buster /assets/img/ada/ada-braze-2.png %}
[4]: {% image_buster /assets/img/ada/ada-braze-3.png %}
[5]: {% image_buster /assets/img/ada/ada-braze-4.png %}