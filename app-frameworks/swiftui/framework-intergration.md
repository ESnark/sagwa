---
description: '기존의 앱에 SwiftUI 뷰를 통합시키고 AppKit, UIKit, WatchKit 뷰와 컨트롤러를 SwiftUI 뷰 계층에 내장시키세요'
---

# 프레임워크 통합

> 원문 출처  
> [https://developer.apple.com/documentation/swiftui/framework\_integration](https://developer.apple.com/documentation/swiftui/framework_integration)

## Summary

> **Framework**
>
> * SwiftUI

## Overview

다음과 같은 방법으로 앱의 현존 컨텐츠와 SwiftUI를 통합하세요:

* AppKit / UIKit / WatchKit View와 View 컨트롤러를 추가할 호스팅 컨트롤러.  호스팅 컨트롤러는 지정된 View 또는 View 컨트롤러를 감싸고 내부 객체와 SwiftUI View 간의 통신을 수월하게 합니다.
* AppKit / UIKit / WatchKit 인터페이스에 SwiftUI View를 추가할 대표 객체. 대표 객체는 SwiftUI View들의 집합을 하나의 form으로 감싸서 스토리보드 기반 앱에 추가할 수 있게 만들어줍니다.

## 주제 <a id="topics"></a>

### Essentials

* [UIKit과 상호작용하기](https://developer.apple.com/tutorials/swiftui/interfacing-with-uikit) SwiftUI는 모든 애플 플랫폼에서 기존 UI 프레임워크와 끊김없이 부드럽게 동작합니다. 예를 들어, UIKit View나 View 컨트롤러를 SwiftUI View 안에 넣을 수 있고 그 반대도 가능합니다.
* [watchOS 앱 만들기](https://developer.apple.com/tutorials/swiftui/creating-a-watchos-app) 이 튜토리얼에서는 여러분이 SwiftUI에 대해서 배운 많은 것들을 적용해볼 수 있으며 아주 적은 노력으로 Landmarks 앱을 watchOS로 마이그레이션할 수 있습니다.

### AppKit Hosting

* _class_ NSHostingController SwiftUI View 세트를 호스팅하는 AppKit View 컨트롤러
* _class_ NSHostingView 하나의 SwiftUI View 계층을 호스팅하는 AppKit View
* _protocol_ NSViewControllerRepresentable AppKit View 컨트롤러를 SwiftUI 인터페이스 안에 통합시킬 때 사용되는 래퍼
* _protocol_ NSViewRepresentable AppKit View를 SwiftUI View 계층에 통합시킬 때 사용되는 래퍼

### UIKit Hosting

* _class_ UIHostingController SwiftUI View 계층을 관리하는 UIKit View 컨트롤러
* _protocol_ UIViewControllerRepresentable UIKit View 컨트롤러를 나타내는 View
* _protocol_ UIViewRepresentable UIKit View를 SwiftUI View 계층에 통합시킬 때 사용되는 래퍼

### WatchKit Hosting

* _class_ WKHostingController SwiftUI View 계층을 호스팅하는 WatchKit 인터페이스 컨트롤러
* _class_ WKUserNotificationHostingController SwiftUI View 계층을 호스팅하는 WatchKit 사용자 노티피케이션 인터페이스 컨트롤러
* _protocol_ WKInterfaceObjectRepresentable UIKit View를 SwiftUI View 계층에 통합시킬 때 사용되는 래퍼

### Deprecated

* Deprecated Symbols 지원되지 않는 심볼과 대안을 리뷰하세요.

## 같이 보기 <a id="see-also"></a>

### 사용자 인터페이스 <a id="user-interface"></a>

* [뷰와 컨트롤](views-and-controls.md) 컨텐츠를 화면에 표시하고 사용자 상호 작용을 처리하세요.
* [뷰 레이아웃과 표현](view-layout-and-presentation.md) 뷰를 스택에 결합하고 뷰 그룹과 리스트를 동적으로 생성하며 뷰 표현과 계층을 정의하세요
* [그리기와 애니메이션](drawing-and-animation.md) 색상, 모양, 그림자와 상태에 따른 커스텀 전환 애니메이션으로 뷰를 강화하세요



