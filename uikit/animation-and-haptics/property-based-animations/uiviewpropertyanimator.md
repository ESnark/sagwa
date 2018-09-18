---
description: 뷰에 대한 변경 사항을 애니메이션화하고 해당 애니메이션의 동적 수정을 허용하는 클래스입니다.
---

# UIViewPropertyAnimator

> 원본출처  
> [https://developer.apple.com/documentation/uikit/uiviewpropertyanimator](https://developer.apple.com/documentation/uikit/uiviewpropertyanimator)

## 개요

UIViewPropertyAnimator 개체를 사용하면 보기 변경 사항을 애니메이션화하고 애니메이션이 끝나기 전에 동적으로 수정할 수 있습니다. 애니메이터를 사용하면 애니메이션 시작부터 끝까지 정상적으로 실행하거나 애니메이션을 대화식 애니메이션으로 전환하여 타이밍을 직접 제어할 수 있습니다. 애니메이터는 [frame](../../../not-found.md), [center](../../../not-found.md), [alpha](../../../not-found.md) 및 [transform](../../../not-found.md) 프로퍼티와 같은 애니메이션 적용 가능한 뷰 특성에 따라 작동하여 블럭에서 필요한 애니메이션을 만듭니다.

PropertyAnimator 객체를 생성할 때는 다음을 지정합니다:

* 하나 이상의 뷰 속성을 수정하는 코드가 포함된 블럭.
* 실행 과정에서 애니메이션의 속도를 정의하는 타이밍 곡선.
* 애니메이션의 지속 시간\(초 단위\)
* 애니메이션이 완료될 때 실행할 선택적 완료 블록

애니메이션 블록에서는 애니메이션 가능한 프로퍼티의 값을 해당 뷰에 반영할 최종 값으로 설정합니다. 예를 들어서 뷰를 페이드 아웃하려면 블럭의 알파값을 0으로 설정합니다. PropertyAnimator 객체는 해당 속성 값을 초기 값에서 블럭에 지정한 새 값으로 조정하는 애니메이션을 생성합니다.

프로퍼티 값이 변경되는 속도는 지정한 타이밍 곡선에 의해서 제어됩니다. 속성 애니메이터는 linear, ease-in, ease-out과 같은 UIKit의 기본 제공 애니메이션 곡선을 지원합니다. 또한 cubic Bezier나 spring 함수를 사용해서 애니메이션 타이밍을 제어할 수도 있습니다.

다음 표준 초기화 메서드를 사용해서 애니메이터를 만드는 경우 애니메이션을 시작하기 위해서는 반드시 [startAnimation\(\)](../../../not-found.md) 메서드를 호출해야 합니다. 만약 애니메이터를 만드는 즉시 실행하고자 한다면 표준 초기화 메서드 대신에 [runningPropertyAnimator\(withDuration:delay:options:animations:completion:\)](../../../not-found.md) 메서드를 사용해야 합니다.

이 클래스는 애니메이션 시작, 중지 및 수정 방법을 정의하는 UIViewAnimating과 UIViewImplicitlyAnimating 프로토콜을 준수합니다. 이 프로토콜들의 메서드에 대한 더 자세한 내용은 [UIViewAnimating](../../../not-found.md)와 [UIViewImplicitlyAnimating](../../../not-found.md)을 참조하세요.

## 애니메이션 동적 수정

PropertyAnimator는 애니메이션의 타이밍과 실행을 프로그래밍적으로 제어합니다. 특히 다음과 같은 작업을 수행할 수 있습니다:

* 애니메이션을 시작, 일시정지, 재개, 중지합니다. [UIViewAnimating](../../../not-found.md) 프로토콜의 메서드를 참조하세요.
* [addAnimations\(\_:\)](../../../not-found.md) 와 [addAnimations\(\_:delayFactor:\)](../../../not-found.md)메서드를 사용해서 원래 애니메이션이 시작된 후 애니메이션 블럭을 추가합니다.
* fractionComplete 프로퍼티를 수정하여 일시 중지된 애니메이션의 위치를 조정할 수 있습니다.
* isReversed 프로퍼티를 사용하여 애니메이션 방향을 변경합니다.
* 애니메이션을 일시정지하고 continueAnimation\(withTimingParameters:durationFactor:\) 메서드를 사용해서 일부 진행된 애니메이션의 타이밍과 애니메이션의 지속시간을 수정합니다.

## 같이 보기

### 애니메이션 상태 가져오기

* var isReversed: Bool

  애니메이션이 반대 방향으로 실행 중인지 나타내는 Boolean 값 

  `Required`

* var state: UIViewAnimatingState

  애니메이션의 현재 상태

  `Required`

* var isRunning: Bool

  애니메이션이 현재 실행 중인지 나타내는 Boolean 값

  `Required`

