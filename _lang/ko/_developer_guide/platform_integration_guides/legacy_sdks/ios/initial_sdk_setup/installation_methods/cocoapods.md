---
nav_title: 코코아팟
article_title: iOS용 코코아팟 통합
platform: iOS
page_order: 2
description: "이 참조 문서에서는 iOS용 CocoaPod를 사용하여 Braze SDK를 통합하는 방법을 설명합니다."

noindex: true
---

{% multi_lang_include 사용 중단/목적-c.md %}

# 코코아팟 통합

## 1단계: 코코아팟 설치

[코코아팟을][apple_initial_setup_1] 통해 iOS SDK를 설치하면 대부분의 설치 과정이 자동화됩니다. 이 프로세스를 시작하기 전에 [Ruby 버전 2.0.0][apple_initial_setup_2] 이상을 사용해야 합니다. 루비 구문에 대한 지식이 없어도 이 SDK를 설치할 수 있으니 걱정하지 마세요.

시작하려면 다음 명령을 실행하세요:

```bash
$ sudo gem install cocoapods
```

코코아팟과 관련된 문제가 있는 경우 코코아팟 \[문제 해결 가이드]\[apple_initial_setup_25]]를 참조하세요.

{% alert note %}
`rake` 실행 파일을 덮어쓰라는 메시지가 표시되면 자세한 내용은 CocoaPods.org 의 [코코아팟 시작하기](http://guides.cocoapods.org/using/getting-started.html "설치") 지침을 참조하세요.
{% endalert %}

## 2단계: 포드파일 구성하기

이제 코코아팟 루비 젬을 설치했으므로 Xcode 프로젝트 디렉토리에 `Podfile` 이라는 파일을 만들어야 합니다.

포드파일에 다음 줄을 추가합니다:

```
target 'YourAppTarget' do
  pod 'Appboy-iOS-SDK'
end
```

부 버전 업데이트보다 작은 버전 업데이트는 자동으로 가져올 수 있도록 Braze 버전을 설정하는 것이 좋습니다. `pod 'Appboy-iOS-SDK' ~> Major.Minor.Build` 처럼 보입니다. 주요 변경 사항이 있는 경우에도 최신 Braze SDK 버전을 자동으로 통합하려면 포드파일에 `pod 'Appboy-iOS-SDK'` 을 사용하면 됩니다.

#### 하위 사양

통합자는 전체 SDK를 가져오는 것이 좋습니다. 그러나 특정 Braze 기능만 통합하려는 것이 확실하다면 전체 SDK 대신 원하는 UI 하위 스펙만 가져올 수 있습니다.

| 하위 사양 | 세부 정보 |
| ------- | ------- |
| `pod 'Appboy-iOS-SDK/InAppMessage'` | `InAppMessage` 하위 스펙에는 Braze 인앱 메시지 UI와 코어 SDK가 포함되어 있습니다.|
| `pod 'Appboy-iOS-SDK/ContentCards'` | `ContentCards` 서브스펙에는 Braze 콘텐츠 카드 UI와 코어 SDK가 포함되어 있습니다. |
| `pod 'Appboy-iOS-SDK/NewsFeed'` | `NewsFeed` 서브스펙에는 Braze Core SDK가 포함되어 있습니다. |
| `pod 'Appboy-iOS-SDK/Core'` | `Core` 하위 스펙에는 사용자 지정 이벤트 및 속성과 같은 분석에 대한 지원이 포함되어 있습니다. |
{: .ws-td-nw-1}

## 3단계: Braze SDK 설치하기

Braze SDK 코코아팟을 설치하려면 터미널에서 Xcode 앱 프로젝트의 디렉토리로 이동하여 다음 명령을 실행합니다:
```
pod install
```

이 시점에서 CocoaPods에서 생성한 새 Xcode 프로젝트 작업 공간을 열 수 있어야 합니다. Xcode 프로젝트 대신 이 Xcode 작업 공간을 사용해야 합니다. 

![Appboy 예제 폴더가 확장되어 새로운 `AppbpyExample.workspace`.]\[apple_initial_setup_15]가 표시됩니다.]

## 다음 단계

[통합을 완료하려면]({{site.baseurl}}/developer_guide/platform_integration_guides/ios/initial_sdk_setup/completing_integration/) 지침을 따르세요.

## CocoaPod를 통해 Braze SDK 업데이트하기

CocoaPod를 업데이트하려면 프로젝트 디렉토리에서 다음 명령을 실행하면 됩니다:

```
pod update
```

[apple_initial_setup_1]: http://cocoapods.org/
[apple_initial_setup_2]: https://www.ruby-lang.org/en/installation/
[apple_initial_setup_3]: http://guides.cocoapods.org/using/getting-started.html "코코아팟 설치 방법"
[apple_initial_setup_5]: https://github.com/braze-inc/braze-ios-sdk/blob/master/AppboyKit/include/Appboy.h
\[apple_initial_setup_15]: {% image_buster /assets/img_archive/podsworkspace.png %}
\[apple_initial_setup_25]: http://guides.cocoapods.org/using/troubleshooting.html "코코아팟 문제 해결 가이드"