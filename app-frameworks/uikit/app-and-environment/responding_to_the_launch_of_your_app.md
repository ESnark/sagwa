---
description: 앱 데이터 구조를 초기화하고 실행시킬 준비를 하세요. 그리고 실행 중에 발생하는 시스템 요청에 대응하세요.
---

# 앱 실행에 대응하기

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/app\_and\_environment/responding\_to\_the\_launch\_of\_your\_app](https://developer.apple.com/documentation/uikit/app_and_environment/responding_to_the_launch_of_your_app)

## 개요 <a id="overview"></a>

운영체제는 사용자가 홈 스크린에 있는 아이콘을 터치할 때 앱을 실행합니다. 여러분의 앱이 특정 이벤트를 요청하는 경우에도 운영체제는 백그라운드에서 앱을 실행하여 해당 이벤트를 처리할 수 있게 해줍니다. 운영체제는 Scene 기반의 앱에도 비슷한 방식을 지원하여 화면에 표시되어야 할 Scene이 있거나 해야 할 일이 있을 때 앱을 실행시킵니다.

모든 앱에는 [UIApplication](uiapplication.md) 객체로 표현되는 연관 프로세스가 존재합니다. 또한 [UIApplicationDelegate](../../../etc/not-found.md) 프로토콜을 준수하는 app delegate 객체는 프로세스 내에서 발생하는 중요한 이벤트에 응답합니다. Scene 기반 앱 역시 app delegate를 사용하여 앱 실행, 종료와 같은 기초적인 이벤트를 관리합니다. 앱 실행 시점에 UIKit은 UIApplication 객체와 app delegate를 자동적으로 생성하며, 그리고 나서 앱의 메인 이벤트 루프가 시작됩니다.



### Launch Storyboard 제공 <a id="provide-a-launch-storyboard"></a>

유저가 기기에서 앱을 처음 실행하면, 운영체제는 앱이 UI 표시할 준비를 하는 동안 Launch storyboard를 보여줍니다. Launch storyboard는 사용자에게 앱이 실행되었고, 무엇인가 하는 중이라는 확신을 줍니다. 만약 앱의 초기화 속도나 UI를 준비하는 시간이 길지 않다면 사용자는 Lauch storyboard를 아주 잠깐만 보게 될 것입니다.

Xcode 프로젝트에는 개발자가 커스터마이즈 할 수 있는 Lauch storyboard가 기본적으로 포함되어 있으며 필요에 따라 다른 Lauch storyboard를 더 추가할 수 있습니다. 프로젝트에 새 Lauch storyboard를 추가하려면 다음 순서에 따라 진행해세요:

1. Xcode에서 프로젝트를 엽니다.
2. File &gt; New &gt; File
3. Lauch Screen 리소스를 프로젝트에 추가합니다.

Launch storyboard에 뷰를 추가하고 오토 레이아웃을 사용해서 크기와 위치를 지정하여 실행될 환경에 적응시키세요. UIKit은 여러분이 사용한 오토 레이아웃 제약조건을 사용하여 뷰를 사용가능한 공간에 맞춰 표시할 것입니다. [Human Interface Guideline](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/launch-screen)을 참조하세요.



{% hint style="info" %}
Important

Launch screen에 정적 이미지를 사용하지 마세요. iOS 14부터 Lauch screen의 용량은 25MB로 제한됩니다.
{% endhint %}

### 앱 데이터 구조 초기화 <a id="initialize-your-apps-data-structures"></a>

앱 실행 초기화 코드에 다음 메소드를 하나 이상 포함시키세요:

* [application\(\_:willFinishLaunchingWithOptions:\)](../../../etc/not-found.md)
* [application\(\_:didFinishLaunchingWithOptions:\)](../../../etc/not-found.md)

UIKit은 앱 실행 사이클 초기에 이 메소드들을 호출하여 다음 용도로 사용합니다:

* 앱 데이터 구조 초기화
* 앱 구동에 필요한 리소스가 있는지 검증
* 앱 최초 실행 시 일회성 설정. 예를 들면 템플릿이나 유저가 수정가능한 파일들을 작성 가능한 디렉토리에 설치합니다. [Performing One-Time Setup for Your App](../../../etc/not-found.md)을 참조하세요.
* 앱이 사용하는 중요한 서비스들 연결. 예를 들어 앱이 원격 노티피케이션을 사용하는 경우 Apple Push Notification 서비스를 연결합니다.
* 앱이 실행된 원인을 파악하기 위해여 Lauch options dictionary를 검사합니다. [앱이 실행된 이유를 확인하기](responding_to_the_launch_of_your_app.md#determine-why-your-app-launched)를 참조하세요

Scene 기반 앱이 아니라면 UIKit은 실행 시점에 자동으로 기본 UI를 로드합니다. application\(\_:didFinishLaunchingWithOptions:\) 메소드를 사용하면 인터페이스가 화면에 나타나기 전 부가적인 변화를 줄 수 있습니다. 예를 들어, 사용자가 지난번에 앱을 사용했을 때 하고 있었던 동작을 반영하는 다른 뷰 컨트롤러를 설치할 수 있습니다.

### 장시간 작업을 메인 스레드에서 제거 <a id="move-long-running-tasks-off-the-main-thread"></a>

빠른 앱 실행 속도는 사용자에게 좋은 인상을 줍니다. 그러나 UIKit은 application\(\_:didFinishLaunchingWithOptions:\) 메소드가 리턴될 때까지 앱의 인터페이스를 표시하지 않기 때문에 [application\(\_:didFinishLaunchingWithOptions:\)](../../../etc/not-found.md)나 [application\(\_:willFinishLaunchingWithOptions:\)](../../../etc/not-found.md)안에서 시간이 오래 걸리는 작업을 수행하는 것은 앱을 느려보이게 만듭니다. 또한 운영체제는 앱의 백그라운드 수행 시간에 제한을 두고 있기 때문에 백그라운드 실행 시에도 빠르게 리턴하는 것은 여전히 중요합니다.

앱 초기화에 중요하지 않은 작업들은 앱 실행 시퀀스에서 제외시키세요:

* 앱에 즉시 필요하지 않은 기능의 초기화는 미루세요.
* 중요하고 장시간 소요되는 작업을 메인 스레드에서 제거하세요. 대안으로는 비동기적으로 작업을 수행할 수 있는 Global dispatch queue 등이 있습니다.

### 앱이 실행된 이유를 확인하기 <a id="determine-why-your-app-launched"></a>

UIKit은 앱을 실행 할때 [application\(\_:willFinishLaunchingWithOptions:\)](../../../etc/not-found.md)와 [application\(\_:didFinishLaunchingWithOptions:\)](../../../etc/not-found.md)에 앱이 실행된 이유에 대한 정보와 함께 Launch options dictionary를 전달합니다. 이 dictionary의 키는 즉시 수행할 중요한 작업을 가리킵니다. 예를 들어, 다른 곳에서 시작하여 이 앱에서 계속 진행하려는 동작에 대한 정보를 반영하고 있을 수 있습니다. Always check the contents of the launch options dictionary for keys that you expect, and respond appropriately to their presence.

{% hint style="info" %}
Note

Scene 기반 앱의 경우, UIKit이 [application\(\_:configurationForConnection:options:\)](../../../etc/not-found.md) 메소드에 전달하는 options를 보고 scene이 왜 생성되었는지를 확인하세요.
{% endhint %}

**Listing 1**은 백그라운드 위치 업데이트를 다루는 앱의 delegate 메소드를 보여줍니다. location 키가 있을 때 앱은 위치 업데이트를 미루지 않고 즉시 수행합니다. 위치 업데이트를 시작함으로써 Core Location 프레임워크가 새로운 location 이벤트를 전달하도록 합니다.

**Listing 1 실행 시 location event에 응답하기**

```swift
class AppDelegate: UIResponder, UIApplicationDelegate, CLLocationManagerDelegate {
    let locationManager = CLLocationManager()
    func application(_ application: UIApplication,
              didFinishLaunchingWithOptions launchOptions:
              [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
       
      // 새 location 데이터 때문에 실행된 것이라면 visits 서비스를 실행합니다.
      if let keys = launchOptions?.keys {
         if keys.contains(.location) {
            locationManager.delegate = self
            locationManager.startMonitoringVisits()
         }
      }
       
      return true
   }
   // other methods…
}
```

앱이 해당 기능을 지원하지 않는다면 시스템은 키를 포함하지 않습니다. 예를 들어 앱이 원격 노티피케이션을 지원하지 않는다면 시스템은 [remoteNotification](../../../etc/not-found.md) 키를 포함하지 않습니다.

Launch option key 리스트와 키를 다루는 방법에 대해서는 [UIApplication.LaunchOptionsKey](../../../etc/not-found.md)를 참조하세요.

## Topics

### 실행 시간

* [앱 실행 시퀀스에 대해서](../../../etc/not-found.md) 앱 실행 시 사용자 코드가 실행되는 순서에 대해서 알아봅시다.
* [앱의 일회성 설정 수행](../../../etc/not-found.md) 앱 환경의 적절한 구성을 보장하세요.
* [앱 실행 간의 UI 보존하기](../../../etc/not-found.md) 시스템이 종료시키기 전의 앱 상태를 반환하세요.

## 같이 보기 <a id="see-also"></a>

### 라이프 사이클 <a id="life-cycle"></a>

* [앱 라이프 사이클 관리하기](managing_your_app_s_life_cycle.md) 앱이 foreground, background 상태에 있을 때 시스템 노티피케이션에 대응하고 시스템과 관련된 중요한 이벤트를 처리하세요.
* _class_ [UIApplication](uiapplication.md) iOS에서 실행되는 앱의 제어와 조정의 중심점
* _protocol_ UIApplicationDelegate 앱 라이프 타임동안 발생하는 중요한 이벤트에 대해 응답하기 위해서 UIApplication 싱글턴 객체가 호출하는 메서드 집합
* Scenes 여러 개의 앱 UI 인스턴스를 동시에 관리하고 리소스를 적절한 인스턴스에 분배하세요.



