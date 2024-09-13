---
nav_title: Google 광고 ID(선택 사항)
article_title: Android용 Google 광고 ID(선택 사항)
page_order: 9
platform: 
  - Android
description: "이 참조 문서에서는 Google 광고 ID와 이 광고 정보를 Android 또는 FireOS 애플리케이션용 Braze에 전달하는 방법에 대해 설명합니다."

---

# Google 광고 ID(Android 전용)

> [Google 광고 ID는][2] Google Play 서비스에서 제공하는 광고용 선택적 사용자별 익명 고유 ID로, 재설정이 가능합니다. 이 참조 문서에서는 Google 광고 ID와 이 광고 정보를 Android 또는 FireOS 애플리케이션용 Braze에 전달하는 방법에 대해 설명합니다.

GAID는 사용자가 자신의 식별자를 재설정하고 Google Play 앱 내에서 관심사 기반 광고를 옵트아웃할 수 있는 기능을 제공하며, 개발자에게는 앱에서 지속적으로 수익을 창출할 수 있는 간단한 표준 시스템을 제공합니다.

## Braze에 Google 광고 ID 전달하기

Google 광고 ID는 Braze SDK에서 자동으로 수집되지 않으며, 수동으로 설정해야 합니다. [`Braze.setGoogleAdvertisingId()`][1] 메서드를 통해 수동으로 설정해야 합니다.

{% alert important %}
Google은 비 UI 스레드에서 광고 ID를 수집하도록 요구합니다.
{% endalert %}

{% tabs %}
{% tab JAVA %}

```java
new Thread(new Runnable() {
  @Override
  public void run() {
    try {
      AdvertisingIdClient.Info idInfo = AdvertisingIdClient.getAdvertisingIdInfo(getApplicationContext());
      Braze.getInstance(getApplicationContext()).setGoogleAdvertisingId(idInfo.getId(), idInfo.isLimitAdTrackingEnabled());
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}).start();
```

{% endtab %}
{% tab KOTLIN %}

```kotlin
Thread(Runnable {
  try {
    val idInfo = AdvertisingIdClient.getAdvertisingIdInfo(getApplicationContext())
    Braze.getInstance(getApplicationContext()).setGoogleAdvertisingId(idInfo.id, idInfo.isLimitAdTrackingEnabled)
  } catch (e: Exception) {
    e.printStackTrace()
  }
}).start()
```

{% endtab %}
{% endtabs %}


[1]: https://braze-inc.github.io/braze-android-sdk/kdoc/braze-android-sdk/com.braze/-i-braze/set-google-advertising-id.html
[2]: https://support.google.com/googleplay/android-developer/answer/6048248/advertising-id?hl=en