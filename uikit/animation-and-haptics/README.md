---
description: 뷰 기반 애니메이션 햅틱을 사용하여 사용자에게 피드백을 제공합니다.
---

# 애니메이션과 햅틱

> 원본출처  
> [https://developer.apple.com/documentation/uikit/animation\_and\_haptics](https://developer.apple.com/documentation/uikit/animation_and_haptics)

## 주제 {#topics}

### 컨텐츠 애니메이션 {#content-animations}

* [프로퍼티 기반 애니메이션 ](property-based-animations/)뷰의 프로퍼티를 바꿈으로써 애니메이션을 만드세요
* [View controller 전환](view-controller.md) 하나의 view controller에서 다른 하나로 넘어가는 커스텀 전환효과를 정의하세요

### 물리 기반 애니메이션 {#physics-based-animations}

* UIKit Dynamics 뷰에 물리 기반 애니메이션을 적용하세요

### 패럴렉스 효과 {#parallax-effects}

* 모션 효과 뷰에 미묘한 동작을 추가해서 3D와 같은 효과를 주세요

### 햅틱 피드백 {#haptic-feedback}

특정 유형의 이벤트에 대응하여 햅틱 피드백을 제공합니다.

* _class_ UIFeedbackGenerator

  모든 피드백 생성기의 추상 슈퍼 클래스입니다.

* _class_ UIImpactFeedbackGenerator

  [UIFeedbackGenerator](../../not-found.md)의 구상 하위 클래스로써 물리적 충격을 시뮬레이션하는 햅틱을 만들어냅니다.

* _class_ UINotificationFeedbackGenerator

  [UIFeedbackGenerator](../../not-found.md)의 구상 하위 클래스로써 성공, 실패, 경고를 전달하는 햅틱을 만들어냅니다.

* _class_ UISelectionFeedbackGenerator

  [UIFeedbackGenerator](../../not-found.md)의 구상 하위 클래스로써 선택항목의 변경을 나타내는 햅틱을 만들어냅니다.

## 같이 보기 {#see-also}

### 유저 인터페이스 {#user-interface}

* [뷰와 컨트롤](../views_and_controls/) 화면에 컨텐츠를 표시하고 해당 컨텐츠에 상호작용을 지정하세요.
* [View Controllers](../view-controllers/) View Controller로 인터페이스를 관리하고 앱 컨텐츠 탐색을 수월하게 만드세요.
* 뷰 레이아웃 Stack View를 사용해서 인터페이스를 자동으로 배치하고 View를 정교하게 배치해야 하는 경우 자동 레이아웃을 사용하세요.
* 윈도우와 스크린

   뷰 계층 구조 및 기타 컨텐츠를 위한 컨테이너를 제공합니다.

