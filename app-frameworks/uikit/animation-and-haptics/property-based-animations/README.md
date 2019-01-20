# 프로퍼티 기반 애니메이션

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/animation\_and\_haptics/property-based\_animations](https://developer.apple.com/documentation/uikit/animation_and_haptics/property-based_animations)

## 주제

### 첫 시작

* _class_ [UIViewPropertyAnimator](uiviewpropertyanimator.md)

  뷰에 대한 변경 사항을 애니메이션화하고 해당 애니메이션의 동적 수정을 허용하는 클래스입니다.

* _protocol_ UIViewAnimating

  커스텀 애니메이터 객체를 구현하기 위한 인터페이스입니다.

### 타이밍 곡선

* protocol UITimingCurveProvider

  애니메이션을 수행하는 데 필요한 타이밍 정보를 제공하는 인터페이스입니다.

* class UISpringTimingParameters

  스프링의 동작을 흉내내는 애니메이션의 타이밍 정보.

* class UICubicTimingParameters

  Cubic Bézier 곡선의 형태로 나타내는 애니메이션에 대한 타이밍 정보.

### 진행중인 애니메이션

* protocol UIViewImplicitlyAnimating

  실행 중인 애니메이션을 수정하기 위한 인터페이스입니다.

## 같이 보기

### 컨텐츠 애니메이션

* [View controller 전환](../view-controller.md) 하나의 view controller에서 다른 하나로 넘어가는 커스텀 전환효과를 정의하세요

