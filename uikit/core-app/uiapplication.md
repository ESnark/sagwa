---
description: iOS에서 실행되는 앱의 제어와 조정의 중심점
---

# UIApplication

> 원본출처  
> [https://developer.apple.com/documentation/uikit/uiapplication](https://developer.apple.com/documentation/uikit/uiapplication)

## 개요

모든 iOS 앱에는 정확히 단 하나의 UIApplication 인스턴스가 존재합니다.\(그러나 매우 드문경우 하위 클래스가 존재하기도 합니다.\) 앱이 시작되면 시스템은 [UIApplicationMain\(\_:\_:\_:\_:\)](../../not-found.md) 함수를 호출합니다. 다른 작업들도 있지만 이 함수는 UIApplication 객체의 [싱글턴](../../not-found.md)을 생성하는 작업을 합니다. 그런 다음 [shared](../../not-found.md) 클래스 메서드를 호출함으로써 해당 싱글턴 객체에 접근할 수 있습니다.

application 객체의 주요 역할은 사용자 이벤트로부터의 초기 라우팅을 처리하는 것입니다. control 객체\([UIControl](../../not-found.md) 클래스의 인스턴스\)가 target 객체에 action 메세지를 보내면 application 객체가 중간에서 전달합니다.

UIApplication 클래스는 UIApplicationDelegate 프로토콜을 준수하고 일부 프로토콜을 필수적으로 구현하는 delegate를 정의합니다. application 객체는 delegate에게 중요한 런타임 이벤트\(예: 앱 시작, 메모리 부족 경고, 앱 종료 등\)를 알리고 적절히 응답할 기회를 제공합니다.

앱은 openURL\(\_:\) 메서드를 통해서 이메일이나 이미지 파일과 같은 리소스를 공동으로 처리할 수 있습니다. 예를 들어 이메일 URL로 이 메서드를 호출하는 앱을 통해 메일 앱이 시작되고 메세지가 표시됩니다.

이 클래스의 API를 사용하면 기기별 동작을 관리할 수 있습니다. UIApplication 객체를 사용하여 다음을 수행합니다:

* 들어오는 터치 이벤트 일시 중단 \([beginIgnoringInteractionEvents\(\)](../../not-found.md)\)
* 원격 노티피케이션에 등록 \([registerForRemoteNotifications\(\)](../../not-found.md)\)
* 실행 취소/다시 실행 UI를 트리거 \([applicationSupportsShakeToEdit](../../not-found.md)\)
* URL 스키마를 처리할 수 있는 설치된 앱이 있는지 확인 \([canOpenURL\(\_:\)](../../not-found.md)\)
* 백그라운드에서 작업을 완료할 수 있도록 앱 실행을 연장 \([beginBackgroundTask\(expirationHandler:\)](../../not-found.md), [beginBackgroundTask\(withName:expirationHandler:\)](../../not-found.md)\)
* 로컬 노티피케이션의 예약과 취소 \([scheduleLocalNotification\(\_:\)](../../not-found.md), [cancelLocalNotification\(\_:\)](../../not-found.md)\)
* 원격제어 이벤트 수신을 조정 \([beginReceivingRemoteControlEvents\(\)](../../not-found.md), [endReceivingRemoteControlEvents\(\)](../../not-found.md)\)
* 앱 수준 상태복원 작업 수행\([상태복원 동작 관리](uiapplication.md#managing_the_state_restoration_behavior) 작업 그룹의 메서드\)

## 서브클래싱 관련 정보 {#subclassing_notes}

대부분의 앱들은 UIApplication을 서브클래싱할 필요가 없습니다. 대신에 App delegate를 사용해서 시스템과 앱간의 상호작용을 관리합니다.

만약 \(매우 드문 경우지만\) 앱이 시스템보다 들어오는 이벤트를 먼저 처리해야 한다면 커스텀 이벤트 또는 action 전송 메커니즘을 직접 구현할 수 있습니다. 이를 위해서 UIApplication을 서브클래싱하고 [sendEvent\(\_:\)](../../not-found.md)나 [sendAction\(\_:to:from:for:\)](../../not-found.md)까지도 오버라이드 할 수 있습니다. 가로채는 모든 이벤트에 대해서 이벤트 처리를 한 후 `super.sendEvent(_:)`를 호출해서 시스템으로 전송하세요. 이벤트를 가로채는 것은 거의 필요하지 않으며 가능하다면 피해야 합니다.

## 주제 {#topics}

### 앱 인스턴스 얻기 {#getting_the_app_instance}

* _class var_ shared: UIApplication 싱글턴 앱 인스턴스를 반환합니다.

### 앱 동작 관리 {#managing_the_apps_behavior}

* _var_ delegate: UIApplicationDelegate?

  앱 객체의 delegate

* _protocol_ UIApplicationDelegate

  앱 라이프 타임동안 발생하는 중요한 이벤트에 대해 응답하기 위해서 UIApplication 싱글턴 객체가 호출하는 메서드 세트

### 원격 노티피케이션 등록하기 {#registering_for_remote_notifications}

* _func_ registerForRemoteNotifications\(\)

  애플 푸시 노티피케이션 서비스를 통해서 원격 노티피케이션을 받도록 등록합니다.

* _func_ unregisterForRemoteNotifications\(\)

  애플 푸시 노티피케이션을 통해 받는 모든 원격 노티피케이션의 등록을 취소합니다.

* _var_ isRegisteredForRemoteNotifications: Bool

  앱이 현재 원격 노티피케이션에 등록되었는지 나타내는 Boolean 값

### 앱 상태 확인하기 {#getting_the_application_state}

* _var_ applicationState: UIApplication.State

  앱의 런타임 상태

* _enum_ UIApplication.State

  앱의 실행 상태

### 백그라운드 실행 관리하기 {#managing_background_execution}

* _var_ backgroundRefreshStatus: UIBackgroundRefreshStatus 백그라운드 동작 수행을 위해 실행될 수 있는 앱의 기능
* _enum_ UIBackgroundRefreshStatus

  앱의 백그라운드 실행 설정 여부를 나타내는 상수

* _func_ beginBackgroundTask\(withName: String?, expirationHandler: \(\(\) -&gt; Void\)? = nil\) -&gt; UIBackgroundTaskIdentifier 장시간동안 실행되는 새로운 백그라운드 작업의 시작을 지정된 이름으로 표시합니다.
* _func_ beginBackgroundTask\(expirationHandler: \(\(\) -&gt; Void\)? = nil\) -&gt; UIBackgroundTaskIdentifier

  장시간 실행되는 새로운 백그라운드 작업을 표시합니다.

* _func_ endBackgroundTask\(UIBackgroundTaskIdentifier\) 특정 장기 실행 백그라운드 작업의 끝을 표시합니다.
* _struct_ UIBackgroundTaskIdentifier 백그라운드에서 실행할 요청을 식별하는 고유한 토큰
* _var_ backgroundTimeRemaining: TimeInterval

  백그라운드에서 앱이 실행될 시간

### 백그라운드에서 컨텐츠 가져오기 {#fetching_content_in_the_background}

* _func_ setMinimumBackgroundFetchInterval\(TimeInterval\)

  백그라운드 가져오기 작업 사이에 대기해야 하는 최소 시간을 지정합니다.

* _class let_ backgroundFetchIntervalMinimum: TimeInterval

  시스템에서 지원하는 가져오기 작업 간 시간 간격의 최소 단위입니다.

* _class let_ backgroundFetchIntervalNever: TimeInterval 가져오기 작업을 막을만큼 큰 시간 간격입니다.
* _let_ UIMinimumKeepAliveTimeout: TimeInterval

  앱이 백그라운드에서 중요한 작업을 실행할 최소 시간\(초 단위\)

### URL 리소스 열기 {#opening_a_url_resource}

* _func_ open\(URL, options: \[UIApplication.OpenExternalURLOptionsKey : Any\] = \[:\], completionHandler: \(\(Bool\) -&gt; Void\)? = nil\) 지정된 URL의 리소스를 여는 작업을 시도합니다.
* _func_ canOpenURL\(URL\) -&gt; Bool 주어진 URL의 스키마를 처리할 수 있는지 나타내는 Boolean 값을 반환합니다.
* _struct_ UIApplication.OpenExternalURLOptionsKey

  URL을 여는 옵션 `Beta`

* _class let_ openSettingsURLString: String openURL\(\_:\) 메서드에 전달할 수 있는 URL을 생성합니다. 이 문자열로 생성된 URL을 열면 시스템에서 Setting 앱을 실행하고 만약 있다면 앱의 커스텀 설정을 보여줍니다.

### 앱 Idle Timer 관리하기 {#managing_the_app_idle_timer}

* _var_ isIdleTimerDisabled: Bool

  앱의 Idle Timer가 비활성화 되었는지를 나타내는 Boolean 값

### 상태복원 동작 관리 {#managing_the_state_restoration_behavior}

* _func_ extendStateRestoration\(\)

  코드가 비동기적으로 상태를 복원중임을 앱에 알립니다.

* _func_ completeStateRestoration\(\)

  코드가 비동기 상태 복원을 완료했음을 앱에 알립니다.

* _func_ ignoreSnapshotOnNextApplicationLaunch\(\) 다음 시작 주기 동안 앱에서 최근 스냅샷 이미지를 사용하지 못하도록 합니다.
* _class func_ registerObject\(forStateRestoration: UIStateRestoring, restorationIdentifier: String\)

  상태 복원 시스템에 사용할 커스텀 객체를 등록합니다.

### 홈 스크린에서의 3D 터치 퀵 액션 관리하기 {#managing_home_screen_quick_actions_for-3-d_touch}

* _var_ shortcutItems: \[UIApplicationShortcutItem\]?

  3D 터치를 지원하는 기기에서 사용할 수 있는 홈 스크린 동적 퀵 액션

### 보호된 컨텐츠의 가용성 결정 {#determining_the_availability_of_protected_content}

* _var_ isProtectedDataAvailable: Bool

  컨텐츠 보호가 활성 상태인지를 나타내는 Boolean 값

### 원격 제어 이벤트 등록 {#registering_for_remote_control_events}

* _func_ beginReceivingRemoteControlEvents\(\)

  앱에 원격 제어 이벤트 수신을 시작하도록 지시합니다.

* _func_ endReceivingRemoteControlEvents\(\)

  앱에 원격 제어 이벤트 수신을 중지하도록 지시합니다.

### 앱 Appearance 제어 {#controlling_app_appearance}

* _var_ statusBarFrame: CGRect

  상태 의 영역을 정의하는 프레임 사각형

* _var_ isNetworkActivityIndicatorVisible: Bool

  네트워크 활동의 표시기를 켜거나 끄는 Boolean 값

* _var_ userInterfaceLayoutDirection: UIUserInterfaceLayoutDirection

  유저 인터페이스의 레이아웃 방향

* _enum_ UIUserInterfaceLayoutDirection

  사용자 인터페이스의 방향 흐름을 지정합니다.

### 이벤트의 제어와 처리 {#controlling_and_handling_events}

* _func_ sendEvent\(UIEvent\)

  앱의 적절한 응답자\(Responder\) 객체에 이벤트를 디스패치합니다.

* _func_ sendAction\(Selector, to: Any?, from: Any?, for: UIEvent?\) -&gt; Bool

  Selector로 식별된 action 메세지를 지정된 target으로 보냅니다.

* _func_ beginIgnoringInteractionEvents\(\)

  수신자에게 터치 관련 이벤트 처리를 중지하도록 지시합니다.

* _func_ endIgnoringInteractionEvents\(\)

  수신자에게 터치 관련 이벤트 처리를 재개하도록 지시합니다.

* _var_ isIgnoringInteractionEvents: Bool

  수신자가 화면터치로 시작된 이벤트를 무시하고 있는지를 나타내는 Boolean 값

* _var_ applicationSupportsShakeToEdit: Bool

  장치를 흔들때 실행 취소-다시 실행 유저 인터페이스가 나타나게 할지 결정하는 Boolean 값

### 앱 아이콘 관리 {#managing_the_apps_icon}

* _var_ applicationIconBadgeNumber: Int 현재 스프링보드에서 앱 아이콘의 배지로 표시되고 있는 숫자
* _var_ supportsAlternateIcons: Bool 앱 아이콘이 변경가능한지를 나타내는 Boolean 값
* _var_ alternateIconName: String? 앱 아이콘의 이름
* _func_ setAlternateIconName\(String?, completionHandler: \(\(Error?\) -&gt; Void\)? = nil\) 앱 아이콘을 변경합니다.

### App window 접근 {#getting_app_windows}

* _var_ keyWindow: UIWindow?

  앱의 key window.

* _var_ windows: \[UIWindow\]

  앱에서 보여지고 숨겨져있는 모든 window

### 폰트 사이징 기본설정 가져오기 {#getting_the_font_sizing_preference}

* _var_ preferredContentSizeCategory: UIContentSizeCategory

  사용자가 선호하는 글꼴 사이징 옵션

* _struct_ UIContentSizeCategory

  컨텐츠의 기본 크기를 나타내는 상수

### 기본 인터페이스 방향 관리하기 {#managing_the_default_interface_orientations}

* _func_ supportedInterfaceOrientations\(for: UIWindow?\) -&gt; UIInterfaceOrientationMask

  지정된 window의 view controller에 사용할 기본 인터페이스 방향 set를 반환합니다.

### 상태바 애니메이션 관리하기 {#managing_status_bar_animations}

* _var_ statusBarOrientationAnimationDuration: TimeInterval

  90도 방향 변경 중 상태 바의 애니메이션 지속 시간\(초 단위\)

### 상수Constants

* _enum_ UIStatusBarStyle

  기기의 상태 바 스타일

* _enum_ UIStatusBarAnimation

  상태 바가 숨겨지거나 나타날때 적용되는 애니메이션

* UserInfo Dictionary Keys

  일부 UIApplication에서 발송한 노티피케이션의 userInfo 딕셔너리 값에 접근하는데 사용되는 딕셔너리 키

* Key for Content Size Change Notifications

  새 컨텐츠 사이즈의 카테고리를 식별하는 키

* Extension Point Identifier Constants

  앱에서 허용하지 않을 확장 지점을 식별하는 상수

* Run Loop Mode for Tracking

  Mode while tracking in controls is taking place.

### 노티피케이션 {#notifications}

모든 UIApplication 노티피케이션은 [shared](../../not-found.md)로부터 반환되는 앱 인스턴스에 의해서 발송됩니다.

* _class let_ backgroundRefreshStatusDidChangeNotification: NSNotification.Name

  백그라운드에서 콘텐츠를 다운로드하는 앱의 상태가 변경될때 발송됩니다.

* _class let_ didBecomeActiveNotification: NSNotification.Name

  앱이 Active 상태가 되었을 때 발송됩니다.

* _class let_ didChangeStatusBarFrameNotification: NSNotification.Name

  상태 바의 프레임이 변경되었을때 발송됩니다.

* _class let_ didChangeStatusBarOrientationNotification: NSNotification.Name

  유저 인터페이스의 방향이 변경되었을때 발송됩니다.

* _class let_ didEnterBackgroundNotification: NSNotification.Name

  앱이 Background에 진입했을때 발송됩니다.

* _class let_ didFinishLaunchingNotification: NSNotification.Name

  앱이 launching을 마친 직후에 발송됩니다.

* _class let_ didReceiveMemoryWarningNotification: NSNotification.Name

  앱이 운영체제로부터 메모리 부족 경고를 받았을때 발송됩니다.

* _class let_ protectedDataDidBecomeAvailableNotification: NSNotification.Name

  보호된 파일이 코드를 통해 접근 가능하게 되었을때 발송됩니다.

* _class let_ protectedDataWillBecomeUnavailableNotification: NSNotification.Name

  보호된 파일이 잠기고 접근불가능하게 되기 직전에 발송됩니다.

* _class let_ significantTimeChangeNotification: NSNotification.Name

  중요한 변화가 발생할때 발송됩니다.\(예: 날짜가 바뀔때\(자정\), 캐리어 시간 업데이트, 일광 절약 시간제 변경\)

* _class let_ userDidTakeScreenshotNotification: NSNotification.Name

  사용자가 홈 버튼과 잠금 버튼을 눌러 스크린샷을 찍을 때 발송됩니다.

* _class let_ willChangeStatusBarOrientationNotification: NSNotification.Name

  앱 인터페이스의 방향이 바뀌려고 할 때 발송됩니다.

* _class let_ willChangeStatusBarFrameNotification: NSNotification.Name

  상태 바의 프레임이 바뀌려고 할 때 발송됩니다.

* _class let_ willEnterForegroundNotification: NSNotification.Name

  앱이 Background 상태에서 Active가 되기 직전에 발송됩니다.

* _class let_ willResignActiveNotification: NSNotification.Name

  앱이 더 이상 Active 상태가 아니고 focus를 잃었을 때 발생됩니다.

* _class let_ willTerminateNotification: NSNotification.Name

  앱이 terminate가 되려고 할 때 발송됩니다.

* _static let_ didChangeNotification: NSNotification.Name

  사용자가 기본 컨텐츠 사이즈를 바꿨을 때 발송됩니다.

### Deprecated Symbols

> 생략

## 관련 문서 {#relationships}

### 상속받은 대상 {#inherits_from}

* [UIResponder](../touches_presses_and_gestures/uiresponder.md)

### 준수하는 프로토콜 {#conforms_to}

* CVarArg
* Equatable
* Hashable
* UIPasteConfigurationSupporting
* UIUserActivityRestoring

## 같이 보기 {#see_also}

### Application

* [앱 라이프 사이클 관리하](managing_your_app_s_life_cycle.md)

  앱 delegate가 앱의 상위 수준 동작을 관리하는 방식을 이해합니다.

* _protocol_ UIApplicationDelegate

  앱 라이프 타임동안 발생하는 중요한 이벤트에 대해 응답하기 위해서 UIApplication 싱글턴 객체가 호출하는 메서드 세트

* 앱과 웹에서 컨텐츠에 링크하도록 허용하기 유니버설 링크를 사용하여 앱 내의 콘텐츠에 연결하고 데이터를 안전하게 공유하세요
* _func_ UIApplicationMain\(Int32, UnsafeMutablePointer?&gt;, String?, String?\) -&gt; Int32 어플리케이션 객체와 delegate를 생성하고 이벤트 사이클을 설정합니다.

