---
nav_title: コンテンツカードについて
article_title: コンテンツカードについて
page_order: 0
description: "この参考記事では、Braze コンテンツカードチャネルの概要と一般的なユースケースについて説明します。"
channel:
  - content cards
search_rank: 4
---

# [![Brazeラーニングコース]({% image_buster /assets/img/bl_icon3.png %})](https://learning.braze.com/messaging-channels-content-cards){: style="float:right;width:120px;border:0;" class="noimgborder"} コンテンツカードについて

> コンテンツカードは、アプリまたは Web サイトのインターフェイスに直接埋め込まれるチャネルです。このため、ネイティブでシームレスなエクスペリエンスの一部のようにユーザーをエンゲージメントさせることができます。コンテンツカードを使用するとさまざまなことができますが、最も一般的な実装はメッセージ受信トレイ、カルーセル、バナーです。

コンテンツカードは、メールやプッシュ通知などの他のチャネルの範囲を拡大するのに最適で、アプリや Web サイトのエクスペリエンスをより詳細にコントロールできるようになります。

{% alert note %}
ニュースフィードツールを使用している場合は、より柔軟でカスタマイズ可能で信頼性の高いコンテンツカードメッセージングチャネルに移行することが推奨されます。ニュースフィードは非推奨になります。詳細については、[移行ガイドを]({{site.baseurl}}/user_guide/message_building_by_channel/content_cards/migrating_from_news_feed/) 参照するか、Braze アカウントマネージャーにお問い合わせください。
{% endalert %}

コンテンツカードはアドオン機能であり、購入する必要があります。コンテンツカードの使用を開始するには、Braze カスタマーサクセスマネージャーまたはサポートチームにお問い合わせください。

## コンテンツカードを使用するメリット

開発者がアプリにコンテンツを組み込む場合と比較して、コンテンツカードを使用する場合のメリットをご紹介します。コンテンツカードを使用するメリットは次のとおりです。

- **セグメンテーションとパーソナライゼーションの容易化:**ユーザーデータは Braze に保存されているため、対象ユーザーを簡単に定義し、コンテンツカードを使用してメッセージをパーソナライズできます。
- **レポートの一元化:**コンテンツカードの分析は Braze で追跡されるため、すべてのキャンペーンを一元的に把握できます。
- **一貫性のあるカスタマージャーニー:**コンテンツカードを Braze の他のチャネルと組み合わせて、一貫性のあるカスタマーエクスペリエンスを作成できます。一般的なユースケースは、プッシュ通知を送信し、プッシュ通知にエンゲージしなかったユーザー向けにその通知をコンテンツカードとしてアプリに保存することです。コンテンツが開発者によってアプリに直接組み込まれている場合、そのコンテンツは残りのメッセージングから隔離されます。
- **コンテンツカードにはオプトインが不要:**アプリ内メッセージと同様に、コンテンツカードには、ユーザーによるオプトインや許可が必要ありません。アプリ内メッセージは許可が不要でも有効期間が短いのに対し、コンテンツ カードは許可が不要で永続的です。つまり、アプリ内メッセージとコンテンツカードを組み合わせたメッセージング戦略は、非常にバランスが取れているということです。
- **メッセージングエクスペリエンスを詳細にコントロール:**コンテンツカードの初期設定については依然として開発者の協力が必要ですが、その後はメッセージ、受信者、タイミングなどを Braze ダッシュボードから直接コントロールできるようになります。

### 数字で見るコンテンツカード

マーケティング担当者は Braze でコンテンツカードを自分で作成するため、アプリやサイトを全面的に作成し直さなくても、メッセージングを更新することで投資対効果を得られます。コンテンツカードの ROI に関して参考になる統計をいくつかご紹介します。

- コンテンツカードは、72時間のウィンドウで売上を伸ばすのにメールよりも**38X**効果的です。\[^1]
- ロイヤルティ登録キャンペーンでコンテンツカードを使用すると、コンバージョンが**5倍**向上します。\[^1]
- プッシュ、アプリ内メッセージ、およびコンテンツカードを介してユーザーにアウトリーチを送信すると、プッシュのみでエンゲージメントされたユーザーと比較して、**6.9X**多くのセッションが発生します。\[^2]
- メール、アプリ内メッセージ、およびコンテンツカードを介してユーザーにアウトリーチを送信すると、メールのみを介してエンゲージされたユーザーと比較して、平均ユーザー寿命が**3.6X**長くなります。\[^2]

## ユースケース

このセクションでは、コンテンツカードの一般的なユースケースについて説明します。

{% alert tip %}
さらにインスピレーションが必要な場合は、[コンテンツカードインスピレーションガイド](https://www.braze.com/resources/reports-and-guides/content-cards-inspiration-guide)の参照を強くお勧めします。このガイドには、紹介プログラム、新製品の発売、サブスクリプションの更新など、20 を超えるカスタマイズ可能なキャンペーンが掲載されています。
{% endalert %}

{% tabs %}
{% tab オンボーディング and next steps %}

新規顧客がアプリや Web サイトを探索するときに、戦略的に配置されたコンテンツカードを使用して、提供するものの価値とメリットを説明します。ホームページ上でコンテンツカードを使用して他のコミュニケーションチャネルにオプトインするよう顧客に奨励し、未処理のオンボーディングタスクをコンテンツカードを利用した専用のオンボーディングタブに保存します。顧客が希望するタスクを完了したら、必ずカードを取り出してください。

<style>
  .imgDiv {
      text-align: center;
    }
</style>

<div class="imgDiv">
<img src="{% image_buster /assets/img_archive/cc_usecase_onboarding.png %}" style="border:0px">
</div>

{% endtab %}
{% tab イベント出席 %}

ユーザーのホームページの上部にコンテンツカードを表示してイベントへの参加を促し、ロケーションターゲティングを使用して潜在顧客のいる場所にリーチします。関連する物理的なイベントにユーザーを招待すると、特にブランドでのこれまでの活動を活用したパーソナライズされたメッセージを使用して、ユーザー向けに特別感を演出できます。

<div class="imgDiv">
<img src="{% image_buster /assets/img_archive/cc_usecase_event.png %}" style="border:0px">
</div>

{% endtab %}
{% tab おすすめ %}

ユーザーの行動や好みに関するデータを使用して、ホームページまたは受信トレイのコンテンツカードから関連コンテンツをリアルタイムで表示し、それらを製品提供に引き込みます。

<div class="imgDiv">
<img src="{% image_buster /assets/img_archive/cc_usecase_recommendation.png %}" style="border:0px">
</div>

{% endtab %}
{% tab 販売とプロモーション %}

コンテンツカードを活用して、ホームページまたは専用のプロモーション受信トレイでプロモーションメッセージやまだ反応のないオファーを直接強調表示します。顧客の以前の購入に基づいて関連コンテンツを取得し、注目を集めるパーソナライズされたプロモーションを提供します。

<div class="imgDiv">
<img src="{% image_buster /assets/img_archive/cc_usecase_promo.png %}" style="border:0px">
</div>

{% endtab %}
{% endtabs %}

### その他のユースケース

これらの主な使用例以外にも、顧客は非常にさまざまな方法でコンテンツカードを使用しています。コンテンツカードの強みはその柔軟性です。必要なユースケースがここに表示されていない場合は、[キーと値のペアを]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/key_value_pairs/)設定して、アプリまたはサイトに送信されるペイロードを取得できます。

## コンテンツカードの配置

このセクションでは、アプリまたはサイト内にコンテンツカードを配置する 3 つの最も一般的な方法を説明します。

- [メッセージの受信トレイ](#message-inbox)
- [カルーセル](#carousel)
- [バナー](#banner)

これらの配置のロジックと実装は Braze のデフォルトではないため、これらのユースケースを実現する作業は、エンジニアリングチームが提供し、サポートする必要があります。これらの配置の実装方法の概要については、[カスタムコンテンツカードの作成に関する記事]({{site.baseurl}}/developer_guide/customization_guides/content_cards/creating_custom_content_cards)を参照してください。

![]({% image_buster /assets/img_archive/cc_placements.png %}){: style="border:0px;"}

### メッセージの受信トレイ

![]({% image_buster /assets/img_archive/cc_placement_inbox.png %}){: style="float:right;margin-left:15px;max-width:30%;border:0px;"}

メッセージ受信ボックス (通知センターまたはフィードとも呼ばれます) は、アプリまたは Web サイト内の永続的な場所であり、コンテンツカードを任意の形式で表示できます。受信トレイ内の各メッセージは、それぞれ独自のコンテンツカードです。 

メッセージ受信トレイは、開発が最小限で済むデフォルトの実装です。iOS、Android、Web 上のメッセージ受信トレイ用の[ビューコントローラー](#how-content-cards-work)が提供されており、コンテンツカードを利用してこの機能を簡単に作成できます。

#### メリット

- ユーザーは一か所で多数のカードを受け取れる
- 他のチャネル (特にプッシュ通知) で見逃した情報や無視した情報を簡単に再表示できる
- オプトインは不要

#### 動作

ユーザーがカードの受信対象者である場合、カードは自動的に受信トレイに表示されます。コンテンツカードは一括表示できるよう構築されているため、ユーザーは対象となるすべてのカードを一度に表示できます。

デフォルトの実装では、受信トレイ内のコンテンツカードは、クラシック (タイトル、テキスト、オプションの画像を含む)、画像のみ、またはキャプション付きの画像カードとして表示されます。アプリ内でメッセージ受信トレイを配置する場所を選択します。

コンテンツカードにはデフォルトのスタイルが付属していますが、アプリのルックアンドフィールに応じてカードとフィードを表示するカスタム実装を選択できます。

### カルーセル

![]({% image_buster /assets/img_archive/cc_politer_carousel.png %}){: style="float:right;margin-left:15px;max-width:30%;border:0px;"}

カルーセルは、顧客がスワイプして表示できる 1 つのスペースに複数のコンテンツを表示します。画像、テキスト、ビデオ、またはそれらすべての組み合わせのスライドショーにすることができます。これはカスタム実装であり、開発者による多少の作業が必要です。

#### メリット

- ユーザーは一か所で多数のカードを受け取れる
- エンゲージメントを高める方法で推奨事項を表示できる

#### 動作

ユーザーがカードを受け取る資格がある場合、カルーセルが追加されたアプリのどのページのカルーセルにもそのカードが表示されます。ユーザーは水平にスワイプして追加の注目カードを表示できます。

これはカスタム実装であるため、開発者と協力してコンテンツカードを表示する独自のビューを構築する必要があります。デフォルトのクラシック、画像のみ、キャプション付き画像カードは、この実装ではサポートされていません。

### バナー

![]({% image_buster /assets/img_archive/cc_placement_banner.png %}){: style="float:right;margin-left:15px;max-width:30%;border:0px;"}

コンテンツカードは動的なバナーとして表示され、ホームページや他の指定ページの上部に永続的に表示されます。

#### メリット

- アプリ内メッセージとは異なりページ上に表示されるため、視聴者にリーチする時間が長くなる
- ホームページの目立つ場所に新しいコンテンツを紹介できる

#### 動作

ユーザーは、対象となる最も関連性の高いコンテンツを表示し、エンゲージできます。これはカスタム実装であるため、開発者と協力してビューをカスタマイズしてコンテンツカードを表示する必要があります。

## コンテンツカードの仕組み

本質的に、コンテンツカードは実際にはデータのペイロードであり、データの外観ではありません。Braze は、最終的にメッセージがどのようなものになるのかを示すコンテンツカードデータを表示するテンプレートビュー (バナー、モーダル、キャプション付き画像) を提供します。

少し技術的な部分を説明しましょう。バックグラウンドでは、コンテンツカードの 3 つの主要な部分があります。

- **モデル:**カードに保存されているデータの種類
- **ビュー:**カードの外観
- **コントローラー:**ユーザーがカードを操作する方法

デフォルトの実装では、ダッシュボードまたは API 経由でカードコンテンツ (モデル) を追加し、ビューとコントローラーはいわゆるビューコントローラーによって処理されます。ビューコントローラーは、アプリケーション全体と画面の間の「接着剤」です。

## コンテンツカードの統合

開発者は、Braze SDK を統合するときにコンテンツカードを統合します。コンテンツカードと統合する方法の詳細については、お使いのプラットフォームの開発者ガイドの記事を参照してください。

- [iOS]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/content_cards/integration/ "iOS コンテンツカード統合ガイド")
- [Android]({{site.baseurl}}/developer_guide/platform_integration_guides/android/content_cards/integration/ "Android コンテンツカード統合ガイド")
- [Web]({{site.baseurl}}/developer_guide/platform_integration_guides/web/content_cards/integration/ "Web コンテンツカード統合ガイド")

## 情報源

<span></span>

\[^1]: [カスタマーリテンションキャンペーンを最大限に活用するための 8 つのヒント](https://www.braze.com/resources/articles/8-tips-for-making-the-most-of-your-customer-retention-campaigns)
\[^2]:[レポート:クロスチャネルマーケティングの違い](https://www.braze.com/resources/reports-and-guides/the-cross-channel-marketing-difference-report)
