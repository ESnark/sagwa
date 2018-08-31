# 앱 라이프 사이클 관리하기

> 원본출처  
> [https://developer.apple.com/documentation/uikit/core\_app/managing\_your\_app\_s\_life\_cycle](https://developer.apple.com/documentation/uikit/core_app/managing_your_app_s_life_cycle)

## 개요 {#overview}

UIKit 앱은 항상 그림 1에 표시된 다섯 가지 상태 중 하나에 있습니다. 앱은 Not Running 상태에서 시작합니다. 사용자가 앱을 시작하면 앱이 잠시 Inactive\(비활성\) 상태로 이동한 후 Active\(활성\) 상태로 진입합니다. \(Active 상태의 앱은 화면상에 나타나고 이것은 foreground 앱으로 불립니다.\) Active 앱을 중단하면 화면 밖으로 이동하며 Background 상태로 전환되어서 잠시 후 시스템이 앱을 Suspend\(일시 중단\)할 때까지 유지됩니다. 시스템은 재량에 따라 Suspend 앱을 종료시켜 Not running 상태로 되돌릴 수 있습니다.



![&#xADF8;&#xB9BC; 1. UIKit &#xC571;&#xC758; &#xC2E4;&#xD589; &#xC0C1;&#xD0DC;](https://docs-assets.developer.apple.com/published/f5ae1a0785/00b28327-17dc-4f0c-866f-29f854edfce3.png)

  
앱의 현재 상태는 사용 가능한 시스템 리소스를 정의합니다. Active 앱은 화면에서 볼 수 있고 사용자 상호작용에 반응해야 하므로 시스템 리소스 사용 시 우선순위를 갖습니다. Background 앱은 화면에 표시되지 않기 때문에 시스템 리소스에 대한 접근과 실행 시간이 제한됩니다.

## 라이프 사이클 이벤트 관리 {#manage_life_cycle_events}

앱이 한 상태에서 다른 상태로 전환할 때 UIKit은 앱 위임 객체\([UIApplicationDelegate](../../not-found.md) 프로토콜을 준수하는 객체\)에 알립니다. App Delegate를 사용하여 새로운 상태와 일치하도록 앱의 동작을 수정하세요. 예를 들어 Not running 상태에서 inactive 상태로 이동할 때 앱 실행 준비에 필요한 작업을 처리합니다.

시스템이 App delegate에 알리는 전환 이벤트는 다음과 같습니다:

* **Launch.** 앱이 Not running에서 Inactive 또는 Background 상태로 전환됩니다. 이 전환을 사용해서 앱의 실행 준비를 하세요. [앱 실행에 응답하기](../../not-found.md) 문서를 참조하세요.
* **Activation.** 앱이 Inactive에서 Active 상태로 전환됩니다. foreground와 화면상에 보이는 상태에서 실행될 준비를 하세요. [Foreground에서 앱 실행할 준비하기](../../not-found.md) 문서를 참조하세요.
* **Deactivation.** 앱이 Active에서 Inactive 상태로 전환됩니다. 일시적으로 앱을 종료하게 됩니다. [Background에서 앱 실행할 준비하기](../../not-found.md) 문서를 참조하세요.
* **Background execution.** Inactive나 Not running 상태에서 Background 상태로 전환됩니다. 화면에서 사라진 상태에서 필수 작업만 처리할 수 있도록 준비하세요. [Background에서 앱 실행할 준비하기](../../not-found.md) 문서를 참조하세요.
* **Termination.** 다른 모든 실행 상태에서 Not running 상태로 전환됩니다. \(Suspended 앱은 terminate 되어도 알림을 받지 못합니다.\) 모든 작업을 취소하고 종료할 준비를 하세요. [applicationWillTerminate\(\_:\)](../../not-found.md) 문서를 참조하세요.

## 동작 이벤트 관리 {#manage_behavioral_events}

App delegate는 다음과 같은 중요한 이벤트에도 응답합니다:

* Memory warning \(메모리 경고\) 앱에서 사용하는 메모리 양을 줄입니다. [메모리 경고에 응답하기](../../not-found.md) 문서를 참조하세요.
* Time changes \(시간 경과\) 앱의 시간에 민감한 기능을 업데이트합니다.
* Protected data becomes available/unavailable \(보호된 데이터가 사용가능/불가능하게 됨\) 사용자가 기기를 잠그거나 해제할 때 파일을 관리합니다.
* State restoration \(상태 복원\) 앱 UI의 이전 상태를 복원함으로써 앱이 멈추지 않고 동작하는 경험을 제공합니다. [시작 시 앱 UI 유지](../../not-found.md) 문서를 참조하세요.
* Handoff tasks \(작업 넘기기\) 다른 기기에서 작업을 계속하기 시작합니다.
* Open URLs \(URL 열기\) 앱으로 전송된 URL을 수신하고 엽니다.
* Inter-app communication \(앱 간 통신\) 페어링 된 watchOS 앱으로부터 데이터를 수신합니다.
* File downloads \(파일 다운로드\) URLSession 객체를 사용하여 다운로드 한 파일을 수신합니다.

App delegate가 라이프 사이클 이벤트를 처리하는 기본 위치이기는 하지만 유일한 장소는 아닙니다. 대부분의 이벤트에서 UIKit은 모든 객체가 관찰할 수 있는 알림을 생성합니다. 관찰할 수 있는 앱 관련 알림 목록을 보려면 [UIApplication](uiapplication.md)을 참조하세요. 이벤트를 처리하는데 사용되는 메서드에 대한 자세한 내용은 [UIApplicationDelegate](../../not-found.md)를 참조하십시오.

## 주제 {#topics}

### 라이프 사이클 이벤트 {#life_cycle_events}

* [앱 실행에 응답하기](../../not-found.md) 앱을 초기화하고 실행할 준비를 합니다.
* [Foreground에서 앱 실행할 준비하기](../../not-found.md) 화면에 나타나도록 앱을 구성합니다.
* [Background에서 앱 실행할 준비하기](../../not-found.md) 앱을 일시 중단할 준비를 합니다.

### 동작 이벤트 {#behavioral_events}

* [메모리 경고에 응답하기](../../not-found.md) 시스템에서 요청하면 메모리를 확보합니다.
* [시작 시 앱 UI 유지](../../not-found.md) 앱이 시스템에 의해 종료된 후 이전 상태로 돌아갑니다.

## 같이 보기 {#see_also}

### Application

* _class_ [UIApplication](uiapplication.md) iOS에서 실행되는 앱의 제어와 조정의 중심점
* _protocol_ UIApplicationDelegate

  앱 라이프 타임동안 발생하는 중요한 이벤트에 대해 응답하기 위해서 UIApplication 싱글턴 객체가 호출하는 메서드 세트

* 앱과 웹에서 컨텐츠에 링크하도록 허용하기 유니버설 링크를 사용하여 앱 내의 콘텐츠에 연결하고 데이터를 안전하게 공유하세요
* _func_ UIApplicationMain\(Int32, UnsafeMutablePointer?&gt;, String?, String?\) -&gt; Int32 어플리케이션 객체와 delegate를 생성하고 이벤트 사이클을 설정합니다.

