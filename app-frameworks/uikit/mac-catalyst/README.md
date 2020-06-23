---
description: 맥 기기에서 사용자가 실행할 수 있는 버전의 아이패드 앱을 만드세요.
---

# Mac Catalyst

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/mac\_catalyst](https://developer.apple.com/documentation/uikit/mac_catalyst)

## Summary

> **Framework**
>
> * UIKit

## 개요 <a id="overview"></a>

Mac Catalyst는 아이패드 앱을 맥 버전으로 만들 수 있게 해줍니다. 아이패드 앱 프로젝트 설정에서 Mac 체크방스를 클릭하는 것으로 맥과 아이패드 버전을 둘다 빌드할 수 있게 됩니다. 이 두 앱은 같은 프로젝트와 소스코드를 공유하기 때문에 코드를 한곳에서 수정하기에 편합니다.

{% hint style="warning" %}
중요

Mac Catalyst로 빌드된 맥 앱은 Mac Catalyst에서 사용 가능한 것으로 명시된 [AppKit](../../../etc/not-found.md) API만 사용할 수 있습니다. \(Ex. [NSToolbar](../../../etc/not-found.md), [NSTouchBar](../../../etc/not-found.md)\) Mac Catalyst는 사용할 수 없는 AppKit API에 대한 액세스를 지원하지 않습니다.
{% endhint %}

아이패드 앱의 맥버전 디자인에 관한 정보는 휴먼 인터페이스 가이드 중의 [Mac Catalyst](https://developer.apple.com/design/human-interface-guidelines/ios/overview/mac-catalyst/)를 살펴보세요.

## 주제 <a id="topics"></a>

### Essentials

* [iPad 앱을 Mac 버전으로 만들기](creating-a-mac-version-of-your-ipad-app.md) Mac Catalyst로 아이패드 앱을 macOS로 가져오세요

### App Support

* 맥 앱의 User Interface Idiom 선택  Mac Catalyst로 만들어진 Mac 앱에서 iPad UI Idiom과 Mac UI Idiom 중에 하나를 선택하세요
* 아이패드 앱의 맥 최적화 macOS의 시스템 기능상 장점을 취하면서 여러분의 아이패드 앱을 맥 앱에 가깝게 만들어 보세요.

### User Interface

* UIKit 카탈로그: 뷰 및 컨트롤의 생성과 커스터마이징 UIKit의 뷰와 컨트롤을 사용해서 앱의 UI를 커스텀하세요.
* Mac Catalyst로 만들어진 맥 앱에서 제목 표시줄 제거하기 제목 표시줄을 제거하고 윈도우 전체를 사용하여 컨텐츠를 표시하세요.
* Toolbar 제목 표시줄 밑, 커스텀 컨텐츠 위에 컨트롤을 위한 공간을 제공합니다.
* Touch Bar 터치바에 상호작용하는 컨텐츠와 컨트롤을 표시합니다.

### User Interactions

* 메뉴바와 UI에 메뉴 및 단축키 추가 Mac Catalyst로 만들어진 맥 앱에 메뉴와 단축키를 추가해서 유용한 동작을 빠르게 실행할 수 있도록 합니다.
* 물리 키보드 입력 처리 사용자가 물리 키보드를 누르고 놓는 동작을 감지합니다.
* _class_ UIHoverGestureRecognizer 뷰 상의 포인터 움직임을 해석하는 이산 제스처 인식기

### User Preferences

* 설정창 표시 Mac Catalyst로 만들어진 맥 앱에 설정창을 제공함으로써 사용자가 Settings 번들에 정의된 설정을 관리할 수 있게 해줍니다.
* 설정창의 변화 감지 컴바인을 사용하여 Mac Catalyst로 만들어진 맥 앱의 사용자 설정 변경에 반응합니다.

## 같이 보기 <a id="see-also"></a>

### 앱 구조 <a id="app_structure"></a>

UIKit은 앱과 시스템의 상호작용을 관리하고 앱의 데이터 및 리소스를 관리할 수 있는 클래스를 제공합니다.

* [앱과 환경](../app-and-environment/) 라이프 사이클 이벤트와 앱 UI Scene을 관리하고 특성과 앱이 실행중인 환경에 대한 정보를 얻으세요.
* [문서, 데이터와 클립보드](../documents-data-pasteboard.md) 앱의 데이터를 구조화하고 클립보드에서 공유하세요.
* 리소스 관리 메인 실행 파일 외부에 저장된 이미지, 문자열, 스토리 보드 및 nib 파일을 관리하세요.
* 앱 확장

  앱의 기본 기능을 시스템의 다른 부분으로 확장하세요.

* 프로세스 간 통신 Handoff를 통해서 데이터를 공유하고 유니버설 링크로 앱의 컨텐츠를 지원하며 행동기반의 서비스를 사용자에게 보여주세요.

