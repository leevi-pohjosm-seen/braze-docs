---
nav_title: 사용자 지정 콘텐츠 카드 만들기
article_title: 사용자 지정 콘텐츠 카드 만들기
page_order: 5
description: "이 문서에서는 사용자 지정 콘텐츠 카드 UI를 만드는 구성 요소에 대해 설명합니다."
channel:
  - content cards
platform:
  - Android
  - FireOS
  - Swift
  - Web
---

# 사용자 지정 콘텐츠 카드 만들기

> 이 문서에서는 사용자 지정 콘텐츠 카드를 구현할 때 사용할 기본 접근 방식과 배너 이미지, 메시지 받은 편지함, 이미지 캐러셀의 세 가지 일반적인 사용 사례에 대해 설명합니다. 기본적으로 수행할 수 있는 작업과 사용자 지정 코드가 필요한 작업을 이해하기 위해 콘텐츠 카드 사용자 지정 가이드의 다른 문서를 이미 읽었다고 가정합니다. 특히 사용자 지정 콘텐츠 카드에 대한 [분석을 기록하는]({{site.baseurl}}/developer_guide/customization_guides/content_cards/logging_analytics) 방법을 이해하기 위한 것입니다. 

Braze는 다양한 [콘텐츠 카드 유형을][1] 제공합니다: `imageOnly`, `captionedImage`, `classic`, `classicImage`, `control`. 이를 구현의 시작점으로 삼아 모양과 느낌을 조정할 수 있습니다. 

Braze 모델의 데이터로 채워진 나만의 프레젠테이션 UI를 만들어 콘텐츠 카드를 완전히 사용자 지정 방식으로 표시할 수도 있습니다. 콘텐츠 카드 개체를 구문 분석하고 페이로드 데이터를 추출합니다. 그런 다음 결과 모델 데이터를 사용하여 [크롤링, 워크, 런 접근 방식의][2]'실행' 단계인 사용자 지정 UI를 채웁니다.

{% alert note %}
각 기본 콘텐츠 카드 유형은 일반 콘텐츠 카드 모델 클래스에서 다른 속성을 상속하는 하위 클래스입니다. 이러한 상속된 속성을 이해하면 사용자 지정 시 유용하게 사용할 수 있습니다. 자세한 내용은 카드 클래스 설명서를 참조하세요[(Android](https://braze-inc.github.io/braze-android-sdk/kdoc/braze-android-sdk/com.braze.models.cards/-card/index.html), [iOS](https://braze-inc.github.io/braze-swift-sdk/documentation/brazekit/braze/contentcard), [웹](https://js.appboycdn.com/web-sdk/latest/doc/classes/braze.card.html)[)](https://braze-inc.github.io/braze-android-sdk/kdoc/braze-android-sdk/com.braze.models.cards/-card/index.html).
{% endalert %}


## 사용자 지정 개요

사용 사례에 따라 사용자 지정 콘텐츠 카드의 정확한 구현 방식은 조금씩 다르지만 이 기본 공식을 따르는 것이 좋습니다:

1. 나만의 UI 구축
2. 데이터 업데이트 듣기
3. 수동 로그 분석

### 1단계: 사용자 지정 UI 만들기 

{% tabs %}
{% tab Android %}

먼저, 나만의 맞춤 조각을 만듭니다. 기본 [`ContentCardFragment`](https://braze-inc.github.io/braze-android-sdk/kdoc/braze-android-sdk/com.braze.ui.contentcards/-content-cards-fragment/index.html) 는 기본 콘텐츠 카드 유형만 처리하도록 설계되었지만 좋은 출발점이 될 수 있습니다.

{% endtab %}
{% tab iOS %}

먼저 사용자 지정 뷰 컨트롤러 컴포넌트를 만듭니다. 기본 [`BrazeContentCardUI.ViewController`](https://braze-inc.github.io/braze-swift-sdk/documentation/brazeui/brazecontentcardui/viewcontroller) 는 기본 콘텐츠 카드 유형만 처리하도록 설계되었지만 좋은 출발점이 될 수 있습니다.

{% endtab %}
{% tab 웹 %}

먼저 카드를 렌더링하는 데 사용할 사용자 지정 HTML 컴포넌트를 만듭니다. 

{% endtab %}
{% endtabs %}

### 2단계: 카드 업데이트 구독

그런 다음 콜백 함수를 등록하여 카드가 새로 고쳐질 때 [데이터 업데이트를 구독합니다][6]. 

### 3단계: 분석 구현

콘텐츠 카드 노출 수, 클릭 수 및 해지 수는 사용자 지정 보기에 자동으로 기록되지 않습니다. 모든 메트릭을 Braze 대시보드 분석에 올바르게 기록하려면 [각각의 방법을 구현해야][3] 합니다.

## 콘텐츠 카드 배치

콘텐츠 카드는 다양한 방식으로 사용할 수 있습니다. 세 가지 일반적인 구현 방법은 메시지 센터, 배너 광고 또는 이미지 캐러셀로 사용하는 것입니다. 이러한 각 배치에 대해 [키-값 쌍][7] (데이터 모델의 `extras` 속성)을 콘텐츠 카드에 할당하고 값에 따라 런타임 중에 카드의 동작, 모양 또는 기능을 동적으로 조정합니다. 

![]({% image_buster /assets/img_archive/cc_placements.png %}){: style="border:0px;"}

### 메시지 받은 편지함

콘텐츠 카드를 사용하여 메시지 센터를 시뮬레이션할 수 있습니다. 이 형식에서 각 메시지는 온클릭 이벤트를 구동하는 [키-값 쌍을][5] 포함하는 자체 카드입니다. 이러한 키-값 쌍은 사용자가 받은 편지함 메시지를 클릭할 때 애플리케이션이 어디로 이동할지 결정할 때 살펴보는 핵심 식별자입니다. 키-값 쌍의 값은 임의로 지정할 수 있습니다. 

다음은 두 개의 메시지 카드를 만드는 데 사용할 수 있는 대시보드 구성의 예입니다. 한 메시지는 사용자가 타겟팅된 읽기 추천을 받기 위해 기본 설정을 추가하도록 하는 클릭 유도 문안이고, 다른 하나는 신규 구독자 세그먼트에 쿠폰 코드를 제공하는 메시지입니다. 

![]({% image_buster /assets/img/content_cards/content-card-message-inbox-with-kvps.png %}){: style="max-width:20%;float:right;margin-left:15px;border:0px;"}

독서 추천 카드의 키-값 쌍의 예는 다음과 같습니다:

- body: 폴리터 위클리 프로필에 관심사를 추가하여 개인별 독서 추천을 받아보세요.
- 스타일: 정보
- 클래스 유형: 알림_센터
- 카드_우선순위: 1

새 구독자 쿠폰의 키-값 쌍의 예는 다음과 같습니다:

- 제목: 무제한 게임 구독
- body: 여름 끝자락 스페셜 - 폴리터 게임 10% 할인 혜택
- 버튼 텍스트: 지금 구독하기
- 스타일: 프로모션
- 클래스 유형: 알림_센터
- 카드_우선순위: 2
- 약관: 신규_구독자_전용

마케팅 담당자는 이 콘텐츠 카드를 신규 사용자 중 일부에게만 제공하도록 설정할 수 있습니다. 

각 값을 처리합니다. `body`, `title`, `buttonText` 과 같은 키에는 마케팅 담당자가 설정할 수 있는 간단한 문자열 값이 있을 수 있습니다. `terms` 같은 키에는 법무 부서에서 승인한 작은 문구 모음을 제공하는 값이 있을 수 있습니다. 앱이나 사이트에서 `style` 및 `class_type` 을 어떻게 렌더링할지 결정합니다. 

{% details Android에 대한 추가 설명 %}

Android 및 FireOS SDK에서 메시지 센터 로직은 Braze의 키-값 쌍으로 제공되는 `class_type` 값에 의해 구동됩니다. 메서드를 사용하여 [`createContentCardable`]({{site.baseurl}}/developer_guide/platform_integration_guides/android/content_cards/implementation_guide) 메서드를 사용하여 이러한 클래스 유형을 필터링하고 식별할 수 있습니다.

{% tabs %}
{% tab Kotlin %}
**클릭 동작에 `class_type` 사용**<br>
콘텐츠 카드 데이터를 사용자 지정 클래스로 인플레이션할 때 데이터의 `ContentCardClass` 속성을 사용하여 데이터를 저장하는 데 어떤 구체적인 하위 클래스를 사용해야 하는지 결정합니다.

```kotlin
 private fun createContentCardable(metadata: Map<String, Any>, type: ContentCardClass?): ContentCardable?{
        return when(type){
            ContentCardClass.AD -> Ad(metadata)
            ContentCardClass.MESSAGE_WEB_VIEW -> WebViewMessage(metadata)
            ContentCardClass.NOTIFICATION_CENTER -> FullPageMessage(metadata)
            ContentCardClass.ITEM_GROUP -> Group(metadata)
            ContentCardClass.ITEM_TILE -> Tile(metadata)
            ContentCardClass.COUPON -> Coupon(metadata)
            else -> null
        }
    }
```

그런 다음 메시지 목록에 대한 사용자 상호작용을 처리할 때 메시지 유형을 사용하여 사용자에게 표시할 보기를 결정할 수 있습니다.

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        //...
        listView.onItemClickListener = AdapterView.OnItemClickListener { parent, view, position, id ->
           when (val card = dataProvider[position]){
                is WebViewMessage -> {
                    val intent = Intent(this, WebViewActivity::class.java)
                    val bundle = Bundle()
                    bundle.putString(WebViewActivity.INTENT_PAYLOAD, card.contentString)
                    intent.putExtras(bundle)
                    startActivity(intent)
                }
                is FullPageMessage -> {
                    val intent = Intent(this, FullPageContentCard::class.java)
                    val bundle = Bundle()
                    bundle.putString(FullPageContentCard.CONTENT_CARD_IMAGE, card.icon)
                    bundle.putString(FullPageContentCard.CONTENT_CARD_TITLE, card.messageTitle)
                    bundle.putString(FullPageContentCard.CONTENT_CARD_DESCRIPTION, card.cardDescription)
                    intent.putExtras(bundle)
                    startActivity(intent)
                }
            }

        }
    }
```
{% endtab %}
{% tab Java %}
**클릭 동작에 `class_type` 사용**<br>
콘텐츠 카드 데이터를 사용자 지정 클래스로 인플레이션할 때 데이터의 `ContentCardClass` 속성을 사용하여 데이터를 저장하는 데 어떤 구체적인 하위 클래스를 사용해야 하는지 결정합니다.

```java
private ContentCardable createContentCardable(Map<String, ?> metadata,  ContentCardClass type){
    switch(type){
        case ContentCardClass.AD:{
            return new Ad(metadata);
        }
        case ContentCardClass.MESSAGE_WEB_VIEW:{
            return new WebViewMessage(metadata);
        }
        case ContentCardClass.NOTIFICATION_CENTER:{
            return new FullPageMessage(metadata);
        }
        case ContentCardClass.ITEM_GROUP:{
            return new Group(metadata);
        }
        case ContentCardClass.ITEM_TILE:{
            return new Tile(metadata);
        }
        case ContentCardClass.COUPON:{
            return new Coupon(metadata);
        }
        default:{
            return null;
        }
    }
}

```

그런 다음 메시지 목록에 대한 사용자 상호작용을 처리할 때 메시지 유형을 사용하여 사용자에게 표시할 보기를 결정할 수 있습니다.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState)
        //...
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id){
               ContentCardable card = dataProvider.get(position);
               if (card instanceof WebViewMessage){
                    Bundle intent = new Intent(this, WebViewActivity.class);
                    Bundle bundle = new Bundle();
                    bundle.putString(WebViewActivity.INTENT_PAYLOAD, card.getContentString());
                    intent.putExtras(bundle);
                    startActivity(intent);
                }
                else if (card instanceof FullPageMessage){
                    Intent intent = new Intent(this, FullPageContentCard.class);
                    Bundle bundle = Bundle();
                    bundle.putString(FullPageContentCard.CONTENT_CARD_IMAGE, card.getIcon());
                    bundle.putString(FullPageContentCard.CONTENT_CARD_TITLE, card.getMessageTitle());
                    bundle.putString(FullPageContentCard.CONTENT_CARD_DESCRIPTION, card.getCardDescription());
                    intent.putExtras(bundle)
                    startActivity(intent)
                }
            }

        });
    }
```

{% endtab %}
{% endtabs %}
{% enddetails %}

### 캐러셀

콘텐츠 카드는 사용자가 가로로 스와이프하여 추가 추천 카드를 볼 수 있는 캐러셀 피드에 설정할 수 있습니다. 

콘텐츠 카드 캐러셀을 만들려면 [콘텐츠 카드의 변경]({{site.baseurl}}/developer_guide/customization_guides/content_cards/customizing_feed/#refreshing-the-feed) 사항을 관찰하고 콘텐츠 카드 도착을 처리하는 로직을 구현합니다. 기본적으로 콘텐츠 카드는 생성 날짜(최신 것부터)를 기준으로 정렬되며, 사용자는 자신이 받을 수 있는 모든 카드를 볼 수 있습니다. 클라이언트 측 로직을 구현하여 캐러셀에 특정 수의 카드를 한 번에 표시할 수 있습니다.

이를 통해 다양한 방식으로 추가 디스플레이 로직을 주문하고 적용할 수 있습니다. 예를 들어 배열에서 처음 다섯 개의 콘텐츠 카드 개체를 선택하거나 키-값 쌍을 도입하여 조건부 논리를 구축할 수 있습니다.

캐러셀을 보조 콘텐츠 카드 피드로 구현하는 경우 [기본 콘텐츠 카드 피드 사용자 지정을]({{site.baseurl}}/developer_guide/customization_guides/content_cards/customizing_feed/#multiple-feeds) 참조하여 키-값 쌍에 따라 카드를 올바른 피드로 정렬하는 방법을 알아보세요.

### 배너

콘텐츠 카드가 꼭 "카드"처럼 보일 필요는 없습니다. 예를 들어 콘텐츠 카드는 홈페이지 또는 지정된 페이지의 상단에 지속적으로 표시되는 동적 배너로 표시될 수 있습니다.

이를 위해 마케팅 담당자는 **이미지 전용** 유형의 콘텐츠 카드로 캠페인 또는 캔버스 단계를 만듭니다. 그런 다음 [콘텐츠 카드를 보조 콘텐츠로][4] 사용하기에 적합한 키-값 쌍을 설정합니다.


[1]: {{site.baseurl}}/user_guide/message_building_by_channel/content_cards/creative_details
[2]: {{site.baseurl}}/developer_guide/customization_guides/customization_overview
[3]: {{site.baseurl}}/developer_guide/customization_guides/content_cards/logging_analytics/#logging-events
[4]: {{site.baseurl}}/developer_guide/customization_guides/content_cards/customizing_behavior/#content-cards-as-supplemental-content
[5]: {{site.baseurl}}/developer_guide/customization_guides/content_cards/customizing_behavior/#key-value-pairs
[6]: {{site.baseurl}}/developer_guide/customization_guides/content_cards/logging_analytics/#listening-for-card-updates
[7]: {{site.baseurl}}/developer_guide/customization_guides/content_cards/customizing_behavior/#key-value-pairs