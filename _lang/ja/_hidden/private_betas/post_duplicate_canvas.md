---
nav_title: "POST:キャンバスの複製"
layout: api_page
page_type: reference
hidden: true
permalink: /api/endpoints/messaging/duplicate_canvases/
description: "この記事では、キャンバスの複製エンドポイントについて詳しく説明します。"
---


# API を使用したキャンバスの複製
{% apimethod post core_エンドポイント|{1} %}
/キャンバス/複製


> このエンドポイントを使用して、キャンバスを複製します。このAPI エンドポイントは、[Braze ダッシュボード][1] のキャンバスの複製に似ています。


API を使用したキャンバスの複製は、現在初期アクセス中です。早いアクセスに参加したい場合は、Braze アカウントマネージャーに連絡してください。
{% endalert %}

## 前提条件

このエンドポイントを使用するには、`canvas.duplicate` 権限を持つAPI キーを生成する必要があります。

## レートリミット

このエンドポイントは、1 分あたり100 個のAPI コールに制限されます。

## Request body

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "canvas_id": (required, string) The Canvas identifier,
  "name": (required, string) The name of the resulting Canvas,
  "description": (optional, string) The description of the resulting Canvas,
  "tag_names": (optional, string) The tags of the resulting Canvas,
}
```

## 要求パラメータ

| パラメータ | required | データ型 | 説明 |
| --------- | ---------| --------- | ----------- |
|| 必須 | string | [キャンバス識別子]({{site.baseurl}}/api/identifier_types/)を参照。 |
|| 必須 | string | 作成されるキャンバスの名前。 |
|| オプション | string | 結果のキャンバスの記述フィールド。 |
| | オプション | string | 作成されるキャンバスのタグ。これらは存在するタグs である必要があります。リクエストに新しいタグs を追加すると、元のキャンバスにあったすべてのタグs が上書きされます。 |


## レスポンス

このエンドポイントは`202` ステータス コードを返し、キャンバスの作成は非同期に行われます。[セキュリティイベントダウン読み込む][2]を使用すると、キャンバスがいつ複製され、どのAPI キーによって記録されたかを確認できます。

[1]: {{site.baseurl}}/user_guide/engagement_tools/campaigns/managing_campaigns/duplicating_segments_and_campaigns#duplicating-segments-campaigns-and-canvases
[2]: {{site.baseurl}}/user_guide/administrative/app_settings/company_settings/security_settings/?redirected=true#security-event-download

