---
nav_title: Braze Go
permalink: "/braze_go/"
hidden: true
noindex: true
hide_toc: true
---

# Braze Go

> Braze・ゴーは、マーケティングチームがどこからでも始めて、どこへでも行けるように、Braze カスタマーエンゲージメント プラットフォームへのアクセスを合理化します。Braze・ゴーは、シンプルかつ効率的に設計されており、特定の新興国向けに設計されています。

{% alert important %}
Braze・ゴーは、一部のマーケットでは利用できません。Braze Go について詳しく知りたい場合は、アカウントマネージャーにお問い合わせください。
{% endalert %}

Braze Go には、Braze と同じ機能がすべて用意されており、以下の機能にフォーカスされた変更が加えられています。 

- 有効なキャンペーン数は最大30 個です。
- アクティブなキャンバスは最大20 個まで設定できます。
- REST API の総デフォルト レート制限は、1 ワークスペースあたり1 時間あたり50,000 です。
    - Braze Go 以外の使用法については、[ REST API limits]({{site.baseurl}}/api/api_limits/#rate-limits-by-request-type) について詳しく説明します。
- キャンペーンとキャンバス間のアクションデータリテンションは2 か月で、復元は行われません。
    - Braze Go 以外の使用法については、[ メッセージング inter アクション data availability]({{site.baseurl}}/messaging_interaction_data/) について詳しく説明します。

{% alert note %}
「キャンペーン」と「キャンバス」のアクション間データは、Snowflakeデータとは異なり、何の影響もありません。
{% endalert %}

- Braze-Braze webhookはサポートされていません。
- 以下のフィルターs は、タグs に関連するものではありません。
    - クリックまたは開かれたキャンペーンまたはキャンバス(タグ付き)
    - キャンペーンまたはキャンバスからタグ付きで最後に受信したメッセージ
    - 受信したキャンペーンまたはタグ付きキャンバス
- また、Brazeは、1年以内に再度実行されなかった1年を超えるイベント、購入、またはその両方を削除する、ユーザープロファイルのイベントおよび購入データのデータリテンションポリシーを実装することもできます。ただし、このデータは、2年間SQLセグメント拡張で引き続き使用できます。

上記のいずれかの機能が更新 d の場合、これはこの記事に反映され、[リリースノート]({{site.baseurl}}/help/release_notes/#most-recent-braze-release-notes) に記載されます。