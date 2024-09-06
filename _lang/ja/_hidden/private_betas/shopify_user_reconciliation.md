---
nav_title: Shopify ユーザー調整
article_title: Shopify ユーザー調整
permalink: "/shopify_user_reconciliation/"
description: "このリファレンス記事では、チェックアウトフローに達したときにユーザーの端末IDと個人情報を照合する方法について説明します。"
hidden: true
---

# チェックアウトフロー外のShopify ユーザー調整 

> Shopifyインテグレーションでは、チェックアウトフローに達したときにユーザーの端末IDと個人情報を照合し、そこでShopify Webhookな事象を実行します。


この機能は現在ベータ版です。興味がある場合は、顧客のサクセスマネージャーまたはアカウントマネージャーにお問い合わせください。
{% endalert %}

Shopifyのサインアップとログインフローによるユーザーの調整をサポートするために、チェックアウトフロー以外のShopifyストアにJavaScript 機能を自動的に実装できます。Braze は、以下の例のように、Shopifyストアに`type="email"` を持つフォームが表示されている場合には、自動的に関数を実装します。

![1]{:style="max-width:60%;"}

この機能が呼び出されると、ウェブ上の匿名ユーザーが、提供されたメールの住所に関連付けられます。今後、当社が使用するShopifyの識別子(ShopifyのカスタマーID、メールアドレス、電話番号など)を参照するすべての行動は、一致があれば同じBraze ユーザーに割り当てられます。

## 考慮事項


Braze は、顧客のShopify サイトの`type="email"` を含むすべてのフォームに精通していません。これは、機能が、ユーザー照合更新に使用されるべき入力フィールドを見逃したり、間違ったフィールドをピックアップして、間違ったメールアドレス(例えば、照会フォーム)をユーザープロファイルに設定する可能性があることを意味します。


Shopify施設でサポートされているすべてのフォームを調査し、このベータソリューションがどのようにしてあなたの要求に効果的に対応できるかを評価することをお勧めします。このベータ機能を利用することで、Shopifyフォームに手動で変更を加えることで、予期しない動作が発生する可能性があることがわかります。

