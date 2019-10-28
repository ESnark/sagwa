---
description: 라이프 사이클 이벤트와 앱 UI Scene을 관리하고 특성과 앱이 실행중인 환경에 대한 정보를 얻으세요.
---

# 앱과 환경

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/app\_and\_environment](https://developer.apple.com/documentation/uikit/app_and_environment)

## Overview

iOS 13부터는 유저가 앱 UI 인스턴스를 동시에 여러개 생성하고 관리할 수 있으며 앱 스위처를 사용하여 앱 간의 이동이 가능합니다. iOS뿐만 아니라 아이패드에서도 여러개의 앱 인스턴스를 나란히 표시할 수 있습니다. 각 UI 인스턴스는 별도의 컨텐츠를 보여주거나 같은 컨텐츠를 다른 방법으로 보여줍니다. 예를 들어 사용자는 하나의 캘린더 앱 인스턴스에서 하루 기준, 그리고 월 기준으로 표시하게 할 수 있습니다.

UIKit은 현재 환경에 대한 세부 정보들을 trait 콜렉션을 사용하여 주고받을 수 있습니다. 이 세부정보들은 기기 설정 조합, 인터페이스 설정, 사용자 설정 등을 반영합니다. 예를 들어 개발자는 현재 뷰, 또는 뷰 컨트롤러에 대해 다크모드가 활성화되었는지 확인하기 위해서 traits를 사용할 수 있습니다. 현재 환경에 따라서 [UIView](../views_and_controls/uiview.md)나 [UIViewController](../view-controllers/uiviewcontroller.md)의 컨텐츠를 커스텀하고자 한다면 해당 UIView, UIViewController 객체의 trait 콜렉션을 참조하세요. 다른 객체에서 trait 변동 노티피케이션을 받고 싶다면 [UITraitEnvironment](../../../etc/not-found.md) 프로토콜을 채택하세요.

## 주제

### 라이프 사이클

* [앱 라이프 사이클 관리하기](managing_your_app_s_life_cycle.md) 앱이 foreground, background 상태에 있을 때 시스템 노티피케이션에 대응하고 시스템과 관련된 중요한 이벤트를 처리하세요.
* 앱 실행에 대응하기 앱 데이터 구조를 초기화하고 실행시킬 준비를 하세요. 그리고 실행 중에 발생하는 시스템 요청에 대응하세요.
* _class_ [UIApplication](uiapplication.md) iOS에서 실행되는 앱의 제어와 조정의 중심점
* _protocol_ UIApplicationDelegate 앱 라이프 타임동안 발생하는 중요한 이벤트에 대해 응답하기 위해서 UIApplication 싱글턴 객체가 호출하는 메서드 집합
* Scenes 여러 개의 앱 UI 인스턴스를 동시에 관리하고 리소스를 적절한 인스턴스에 분배하세요.

### 기기 환경

* _class_ UIDevice 현재 기기를 나타냅니다.
* class UIStatusBarManager 상태바의 구성요소를 설명하는 객체

### Adaptivity

* Apple TV 디스플레이 모드 변경에 대응하기 기기의 스크린 영역 변동에 따라서 이미지와 리소스를 동적으로 바꾸세요
* _class_ UITraitCollection 수평 및 수직 사이즈 클래스, 디스플레이 스케일 및 사용자 인터페이스 종류\(phone, pad, tv 등\)와 같은 특성에 의해 정의되는 앱의 iOS 인터페이스 환경.
* _protocol_ UITraitEnvironment 앱에서 iOS 인터페이스 환경을 사용할 수 있게 해주는 메드 집합
* _protocol_ UIAdaptivePresentationControllerDelegate Presentation 컨트롤러와 함께 앱의 trait 변화에 대응하는 방법을 결정하는 메서드 집합
* _protocol_ UIContentContainer 뷰 컨트롤러의 컨텐츠가 크기와 trait 변화에 적응할 수 있도록 돕는 메서드 집합

### Guided Access

* _protocol_ UIGuidedAccessRestrictionDelegate

  개발자가 Guided Access 기능에 커스텀 제한사항을 추가하는데 사용되는 메서드 집합

* _static func_ guidedAccessRestrictionState\(forIdentifier: String\) -&gt; UIAccessibility.GuidedAccessRestrictionState

  지정된 Guided access 제한에 대한 제한 상태를 반환합니다.

### Architecture

* 앱 32비트 아키텍처에서 64비트 아키텍처로 업데이트 하기 앱이 차기 버전의 운영체제에서 의도한대로 동작할 수 있게 합니다.
* _func_ UIApplicationMain\(Int32, UnsafeMutablePointer&lt;UnsafeMutablePointer&lt;Int8&gt;?&gt;, String?, String?\) -&gt; Int32 어플리케이션 객체와 delegate를 생성하고 이벤트 사이클을 설정합니다.

\_\_

## 같이 보기

### 앱 구조

* [문서, 데이터와 클립보드](../documents-data-pasteboard.md) 앱의 데이터를 구조화하고 클립보드에서 공유하세요
* 리소스 관리 메인 실행 파일 외부에 저장된 이미지, 문자열, 스토리 보드 및 nib 파일을 관리하세요
* 앱 확장

  앱의 기본 기능을 시스템의 다른 부분으로 확장하세요

* 프로세스 간 통신 Handoff를 통해서 데이터를 공유하고 유니버설 링크로 앱의 컨텐츠를 지원하며 행동기반의 서비스를 사용자에게 보여주세요
* Mac Catalyst 맥 기기에서 사용자가 실행할 수 있는 버전의 아이패드 앱을 만드세요.

