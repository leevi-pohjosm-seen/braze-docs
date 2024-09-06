---
nav_title: ドラッグアンドドロップランディングページ
article_title: ドラッグアンドドロップのランディングページを作成する
description: "この記事では、ドラッグアンドドロップエディタを使用してBrazeランディングページを作成およびカスタマイズする方法について説明します。"
page_order: 31
hidden: true
alias: /landing_pages/drag_and_drop/
---

# ドラッグアンドドロップのランディングページ

> ドラッグアンドドロップエディタを使用すると、オーディエンスを増やし、Brazeで直接好みを収集するためのランディングページを作成およびカスタマイズできます。

{% alert important %}
ランディングページは現在ベータ版です。このベータ版に参加することに興味がある場合は、Brazeのアカウントマネージャーに連絡してください。
{% endalert %}

## ランディングページの作成（ドラッグアンドドロップ）

### ステップ 1:ランディングページを作成する

**メッセージング** > **ランディングページ** に移動し、**ランディングページを作成** を選択するか、既存のランディングページの名前を選択して複製または変更します。

![「ランディングページ」のホームページ。][2]{: style="max-width:90%;"}

### ステップ2:ランディングページの詳細を設定する

#### 一般的な詳細

ランディングページの名前と説明は、内部ワークスペースでページを検索するために使用されます。これらはお客様には表示されません。

#### サイトの詳細

メタタグを設定して、ブラウザタブに表示されるページの外観をカスタマイズし、検索エンジンの結果を最適化します。これらはお客様に表示されます。

これらのベストプラクティスに従うことをお勧めします:

| 詳細 | 説明 | おすすめ |
| --- | --- |
| サイトのタイトル | ブラウザタブに表示されるタイトル。 | 60文字まで使用してください。 |
| サイトの説明 | 検索結果に表示されるテキストスニペット。 | 140〜160文字の間で使用してください。|
| ファビコン | ブラウザタブのサイトタイトルの横に表示されるアイコン。 | アスペクト比を1:1にし、サポートされているファイルタイプはPNG、JPEG、またはICOにしてください。 |
| URLハンドル | これは、ユーザーがランディングページに移動するためにクリックするリンクです。 | これはユニークでなければなりません。 |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3}

{% alert note %}
ベータ版の間はカスタムサブドメインのサポートは利用できません。
{% endalert %}

### ステップ 3:ランディングページをカスタマイズする

**エディターを起動**を選択して、ドラッグアンドドロップエディターでランディングページのデザインを開始します。エディタは、カスタマイズしてユースケースに合わせることができるデフォルトのテンプレートでプリロードされます。

![顧客サインアップ用フォーム付きランディングページテンプレート。][8]{: style="max-width:90%;"}

#### ドラッグアンドドロップブロック

エディターはランディングページの構成に2種類のコンポーネントを使用します：行とブロック。すべてのブロックは一列に配置する必要があります。

![「行」と「フォームブロック」を含む「ビルド」エディターセクション。][4]{: style="max-width:30%;"}

#### フォームブロック

フォームブロックを含める場合は、**ボタンがクリックされたときにフォームを送信**するために、トグルがオンになっているボタンを少なくとも1つ含める必要があります。また、[確認状態](#confirmation-state)のための別のランディングページも作成する必要があります。

![新しい顧客を登録し、メールに割引コードを送信するフォームブロックです。][5]{: style="max-width:70%;"}

#### ページコンテナのスタイル

ランディングページのすべての関連コンポーネントブロックに適用されるスタイルは、**ページコンテナ**タブから設定できます。これらのスタイルは、特定のブロックで上書きする場合を除き、ページのどこにでも使用されます。

ページコンテナレベルのスタイルをカスタマイズする前に、設定スタイルを設定することをお勧めします。ページ全体にバックグラウンド画像を追加することもできます。

![背景画像、色、境界線の詳細、コンテンツのスタイリングをカスタマイズするためのオプションを備えたページコンテナ。][6]{: style="max-width:30%;"}

### ステップ 4:{プレビュー}あなたのランディングページ

エディターの**プレビュー**タブでランディングページをプレビューできますが、ベータ版では機能のテストは無効になっています。ランディングページを下書きとして保存した後、**ランディングページ**にアクセスして、ランディングページの横にある**URLをコピー**を選択することで、URLにアクセスできます。共同作業者とURLを共有することもできます。

![メニューが開封されて「URLをコピー」オプションを表示するランディングページ。][7]{: style="max-width:90%;"}

ランディングページに満足したら、**ランディングページを公開**を選択します。

{% alert important %}
URLハンドルはランディングページが公開された後に編集することはできません。
{% endalert %}

## 確認ランディングページの作成 {#confirmation-state}

ランディングページに[フォーム](#form-block)を含める場合は、確認用のランディングページを作成することを忘れないでください。確認状態のための別のランディングページを作成し、フォームを送信するボタンの**開封Web URL**フィールドにリンクを追加します。

## ランディングページへのリンク

ベータ版では、リンクをコピーしてBrazeメッセージやソーシャルメディアキャンペーンに貼り付けることで、任意のチャネルにランディングページへのリンクを含めることができます。

## フォーム送信エラーの処理

ユーザーが無効なフォーム値（受け入れられない特殊文字など）を入力すると、カスタマイズできない一般的なエラーインジケーターが表示され、フォームを送信できません。プレビューランディングページでエラーの動作を確認できます。

## ランディングページから作成されたユーザーの統合

ベータ版の間、ランディングページでの各フォーム送信は、Brazeに新しい匿名のユーザープロファイルを作成します。同じメールアドレスを持つユーザーが既に存在する場合、新しいユーザープロファイルを既存のプロファイルに[`/users/merge`]({{site.baseurl}}/api/endpoints/user_data/post_users_merge#merging-unidentified-user)エンドポイントを使用してマージできます。Braze でユーザーを重複排除するさまざまな方法について学ぶには、[重複ユーザー]({{site.baseurl}}/user_guide/engagement_tools/segments/user_profiles/duplicate_users)を参照してください。

## 考慮事項

- ランディングページの本文サイズは最大1MBです。

## よくある質問

### ランディングページでユーザーが情報を送信するとどうなりますか？

ユーザーがフォームを送信すると、送信されたユーザーデータで新しいBrazeユーザープロファイルが作成されます。

{% alert note %}
ベータ版の間、Brazeはランディングページのどこでユーザーがクリックしても、フォーム送信ごとに新しいユーザーを作成します。
{% endalert %}

### ランディングページを公開するための技術的な要件はありますか？

いいえ、技術的な要件はありません。

### ランディングページ用のHTMLエディターはありますか？

いいえ、これは現在利用できません。

### ランディングページのレポートは利用できますか？

いいえ、これは現在利用できません。

### ランディングページ用のHTMLエディターはありますか？

いいえ、これは現在利用できません。エディターでカスタムコードブロックを使用できます。

[1]: {% image_buster /assets/img/landing_pages/homepage.gif %}
[2]: {% image_buster /assets/img/landing_pages/create.png %}
[3]: {% image_buster /assets/img/landing_pages/details.png %}
[4]: {% image_buster /assets/img/landing_pages/dnd.png %}
[5]: {% image_buster /assets/img/landing_pages/form.png %}
[6]: {% image_buster /assets/img/landing_pages/page_container.png %}
[7]: {% image_buster /assets/img/landing_pages/url_handle.png %}
[8]: {% image_buster /assets/img/landing_pages/template.png %}