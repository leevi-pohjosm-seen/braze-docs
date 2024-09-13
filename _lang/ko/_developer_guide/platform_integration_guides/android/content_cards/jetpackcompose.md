---
nav_title: 제트팩 컴포지션
article_title: 젯팩 컴포즈를 사용한 Android 및 FireOS용 콘텐츠 카드 통합
page_order: 1
platform: 
  - Android
  - FireOS
description: "이 참조 문서에서는 Android 또는 FireOS 애플리케이션용 Jetpack Compose를 사용한 콘텐츠 카드 통합에 대해 설명합니다."
channel:
  - content cards
search_rank: 1
---

# 제트팩 컴포즈가 포함된 콘텐츠 카드

> 이 참조 문서에서는 Android 또는 FireOS 애플리케이션용 Jetpack Compose를 사용한 콘텐츠 카드 통합에 대해 설명합니다.

Android에서는 `ContentCardsList()` 을 사용하여 콘텐츠 카드 피드를 작성 애플리케이션에 추가할 수 있습니다. 예를 들어, 다음과 같습니다.

```kotlin
setContent {
    ContentCardsList()
}
```

### 콘텐츠 카드 스타일링

두 가지 방법 중 하나로 스타일링을 적용할 수 있습니다. 첫 번째는 다음 예제에서처럼 `ContentCardListStyling` 및 `ContentCardStyling` 을 `ContentCardsList()` 으로 전달하는 것입니다:

```kotlin
ContentCardsList(
    style = ContentCardListStyling(listBackgroundColor = Color.Red),
    cardStyle = ContentCardStyling(
        titleTextStyle = TextStyle(
            fontFamily = fontFamily,
            fontSize = 25.sp
        ),
        shadowRadius = 10.dp,
        shortNewsContentCardStyle = BrazeShortNewsContentCardStyling(
            shadowRadius = 15.dp
        )
    )
)
```

두 번째는 다음 예시와 같이 `BrazeStyle` 을 사용하여 Braze 컴포넌트에 대한 글로벌 스타일링을 생성하는 것입니다:

```kotlin
BrazeStyle(
    contentCardStyle = ContentCardStyling(
        textAnnouncementContentCardStyle = BrazeTextAnnouncementContentCardStyling(
            cardBackgroundColor = Color.Red,
            descriptionTextStyle = TextStyle(
                fontFamily = fontFamily,
                fontSize = 25.sp,
            )
        ),
        titleTextColor = Color.Magenta
    )
) {
    // Your app here, including any ContentCardsList() in it
}
```

### 추가 사용자 지정

#### 카드 클릭 처리

카드 클릭을 처리하려면 `Card` 를 받아 `Boolean` 을 `onCardClicked` 로 반환하는 함수를 전달합니다. `true` 이 반환되면 Braze는 분석을 위해 로깅하는 것 외에 클릭에 대한 어떠한 처리도 하지 않습니다. `false` 이 반환되면 Braze가 클릭을 처리합니다.

```kotlin
ContentCardsList(
    onCardClicked = { card ->
        if (card.extras.containsKey("mySpecialKey")) {
            // handle the click here
            true
        } else {
            // Let Braze handle the click
            false
        }
    }
)
```

#### 해고에 대한 알림 사용 설정하기

카드가 해지될 때 알림을 받으려면 `onCardDismissed` 함수에 함수를 전달하세요.

```kotlin
ContentCardsList(
    onCardDismissed = { card ->
        // Do what you need with the card
    }
)
```