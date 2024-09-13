---
nav_title: 사용자 지정 이벤트 추적
article_title: iOS용 사용자 지정 이벤트 추적
platform: iOS
page_order: 2
description: "이 참조 문서에서는 iOS 애플리케이션에 사용자 지정 이벤트를 추가하고 추적하는 방법에 대해 설명합니다."

noindex: true
---

{% multi_lang_include 사용 중단/목적-c.md %}

# iOS용 사용자 지정 이벤트 추적

Braze에서 사용자 지정 이벤트를 기록하여 앱의 사용 패턴에 대해 자세히 알아보고 대시보드에서 사용자의 행동에 따라 사용자를 세분화할 수 있습니다.

구현하기 전에 사용자 지정 이벤트, 사용자 지정 속성 및 구매 이벤트가 제공하는 세분화 옵션의 예와 [이벤트 명명 규칙에]({{site.baseurl}}/user_guide/data_and_analytics/custom_data/event_naming_conventions/) 대한 참고 사항을 [모범 사례에서][0] 검토하세요.

## 사용자 지정 이벤트 추가하기

{% tabs %}
{% tab 목표-C %}

```objc
[[Appboy sharedInstance] logCustomEvent:@"YOUR_EVENT_NAME"];
```

{% endtab %}
{% tab swift %}

```swift
Appboy.sharedInstance()?.logCustomEvent("YOUR_EVENT_NAME")
```

{% endtab %}
{% endtabs %}

### 속성 추가

`NSNumber`, `NSString`, 또는 `NSDate` 값으로 채워진 `NSDictionary` 을 전달하여 사용자 지정 이벤트에 대한 메타데이터를 추가할 수 있습니다.

{% tabs %}
{% tab 목표-C %}

```objc
[[Appboy sharedInstance] logCustomEvent:@"YOUR-EVENT-NAME"
                         withProperties:@{
  @"you": @"can",
  @"pass": @(NO),
  @"orNumbers": @42,
  @"orDates": [NSDate date],
  @"or": @[@"any", @"array", @"here"],
  @"andEven": @{
    @"deeply": @[@"nested", @"json"]
  }
}];
```

{% endtab %}
{% tab swift %}

```swift
Appboy.sharedInstance()?.logCustomEvent(
  "YOUR-EVENT-NAME",
  withProperties: [
    "you": "can",
    "pass": false,
    "orNumbers": 42,
    "orDates": Date(),
    "or": ["any", "array", "here"],
    "andEven": [
      "deeply": ["nested", "json"]
    ]
  ]
)
```

{% endtab %}
{% endtabs %}

자세한 내용은 [클래스 설명서를][4] 참조하세요.

### 예약 키 {#event-reserved-keys}

다음 키는 예약되어 있으며 사용자 지정 이벤트 속성으로 사용할 수 없습니다:

- `time`
- `event_name`

## 추가 리소스

- `Appboy.h` [파일][2] 내의 메서드 선언을 참조하세요. 
- 자세한 내용은 [`logCustomEvent`][3] 문서를 참조하세요.

[0]: {{site.baseurl}}/developer_guide/platform_wide/analytics_overview/#user-data-collection
[2]: https://github.com/Appboy/appboy-ios-sdk/blob/master/AppboyKit/include/Appboy.h
[3]: http://appboy.github.io/appboy-ios-sdk/docs/interface_appboy.html#ad80c39e8c96482a77562a5b1a1d387aa "로그 커스텀 이벤트 문서"
[4]: http://appboy.github.io/appboy-ios-sdk/docs/interface_appboy.html#a4f0051d73d85cb37f63c232248124c79 "로그 커스텀 이벤트:위드프로퍼티 문서"