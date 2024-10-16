---
nav_title: セグメント内の欠落ユーザー
article_title: セグメント内の欠落ユーザー
page_order: 1

page_type: solution
description: "このヘルプ記事では、セグメントに表示されるユーザーがゼロであるにもかかわらず、さらに多くのユーザーが表示されることが予想される場合のトラブルシューティング手順を説明する。"
tool: Segments
---

# セグメント内の欠落ユーザー

`0` 、それ以上のユーザーを見込んでいる場合、2つの解決策が考えられる：
* [正確な統計量を計算する](#calculate-exact-statistics)
* [データ転送を確認する](#verify-data-transfer)

## 正確な統計量を計算する

セグメント統計は推定値を示している可能性がある。推定値は、無作為標本に基づいて算出され、その結果が`+/- 1%` 以内であるという95％の信頼区間がある。ユーザーベースが小さければ小さいほど、セグメントのサイズは概算である可能性が高くなる。**セグメントの詳細**パネルで**正確な統計を計算を**クリックする。これにより、セグメント内の正確なユーザー数が計算される。

![正確な統計を計算するオプションを表示するセグメントの詳細パネル][28]

## データ転送を確認する

フィルタリングしているデータがBrazeに送信されていない可能性がある。どのカスタムイベントがBrazeに送信されているかを確認するには、[カスタムイベントレポートを][1]参照する。

カスタムイベントを特定の日付とアプリとともに選択し、Brazeに実際に転送されているデータを確認する。`0` データがBrazeに送信されていることに気づいたら、次のステップは、Brazeにどのようにイベントを送信しているかを評価することである。

![カスタムイベントのカウントをゼロとして表示するグラフ][29]

{% alert important %}
Brazeダッシュボードに表示されるデータは、Brazeに送信しているものと同じ構文でない場合がある。この2つが正確に一致していることを確認する。
{% endalert %}

まだ助けが必要か？[サポートチケットを]({{site.baseurl}}/braze_support/)開く。

_最終更新日：2021年1月5日_

[1]: {{site.baseurl}}/user_guide/data_and_analytics/custom_data/custom_events/#custom-event-analytics
[28]: {% image_buster /assets/img_archive/trouble8.png %}
[29]: {% image_buster /assets/img_archive/trouble9.png %}
