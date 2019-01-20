# View controller 전환

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/animation\_and\_haptics/view\_controller\_transitions](https://developer.apple.com/documentation/uikit/animation_and_haptics/view_controller_transitions)

## 주제

### 애니메이션 Delegate

* protocol UIViewControllerTransitioningDelegate

  뷰 컨트롤러간의 고정길이 또는 대화식 전환을 관리하는데 사용되는 메서드 집합

### 비 대화식 전환

* protocol UIViewControllerAnimatedTransitioning

  view controller의 커스텀 전환을 구현하는데 사용되는 메서드 집합

* protocol UIViewControllerContextTransitioning

  view controller간에 전환 애니메이션을 위한 컨텍스트 정보를 제공하는 메서드 집합

### 대화식 전환

* class UIPercentDrivenInteractiveTransition

  두 개의 view controller 사이에서 대화형 애니메이션을 구동하는 객체

* protocol UIViewControllerInteractiveTransitioning

  \(네비게이션 컨트롤러 같은\) 객체가 view controller 전환을 구동할 수 있게 하는 메서드 집합

* protocol UIViewImplicitlyAnimating

  실행중인 애니메이션을 수정하기 위한 인터페이스

### 전환 조정자

* protocol UIViewControllerTransitionCoordinator

  view controller 전환과 관련된 애니메이션을 지원하는 메서드 집합

* protocol UIViewControllerTransitionCoordinatorContext 진행 중인 view controller 전환에 대한 정보를 제공하는 메서드 집합

## 같이 보기

### 컨텐츠 애니메이션

* [프로퍼티 기반 애니메이션](property-based-animations/) 뷰의 프로퍼티를 바꿈으로써 애니메이션을 만드세요



