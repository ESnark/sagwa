---
description: 구상 제스처 인식기의 기본 클래스
---

# UIGestureRecognizer

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uigesturerecognizer](https://developer.apple.com/documentation/uikit/uigesturerecognizer)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class UIGestureRecognizer : NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface UIGestureRecognizer : NSObject
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 3.2+
> * tvOS 9.0+
>
> **Framework**
>
> * UIKit

## 개요 <a id="overview"></a>

제스처 인식기 객체\(간단히 제스처 인식기\)는 터치\(또는 다른 입력\)의 연속을 인식하는 로직과 인식에 기반한 동작 로직을 분리시킵니다. 이 객체 중 하나가 일반적인 제스처나 제스처의 변경을 인지하면 객체는 지정된 타겟 객체에 동작 메세지를 보냅니다.

UIGestureRecognizer의 구상 서브클래스는 다음과 같습니다:

* UITapGestureRecognizer
* UIPinchGestureRecognizer
* UIRotationGestureRecognizer
* UISwipeGestureRecognizer
* [UIPanGestureRecognizer](uipangesturerecognizer/)
* UIScreenEdgePanGestureRecognizer
* [UILongPressGestureRecognizer](uilongpressgesturerecognizer.md)

UIGestureRecognizer 클래스는 모든 구상 제스처 인식기에 대해서 설정 가능한 공통 동작들을 정의하고 있습니다. 또한 \([UIGestureRecognizerDelegate](../../../etc/not-found.md) 프로토콜을 준수하는 객체와\) delegate를 통해서 통신하는 것이 가능하므로 일부 동작을 세밀하게 커스텀할 수 있습니다.

제스처 인식기는 특정 뷰와 해당 뷰의 모든 하위 뷰의 hit-test를 거친 터치에 대해서 동작합니다. 따라서 반드시 해당 뷰와 연결되어 있어야 하며 이 연관 관계를 만들기 위해서는 [addGestureRecognizer\(\_:\)](../../../etc/not-found.md)라는 [UIView](../views_and_controls/uiview.md) 메서드를 호출해야 합니다. 제스처 인식기는 뷰의 응답자 체인에 포함되지 않습니다.

제스처 인식기는 연관되어 있는 하나 이상의 타겟-액션 쌍을 가지고 있습니다. 여러개의 타겟-액션 쌍은 개별적이며 누적되지 않습니다. 제스처가 인식되면 연관된 쌍의 각 타겟에 동작 메세지를 전송합니다. 호출된 액션 매서드는 다음 중 하나를 반드시 준수해야 합니다:

```swift
@IBAction func myActionMethod()
@IBAction func myActionMethod(_ sender: UIGestureRecognizer)
```

후자를 준수하는 메서드는 제스처 인식기에 메세지를 전송하여 추가적인 정보를 요청할 수 있습니다. 예를 들어 타겟이 [UIRotationGestureRecognizer](../../../etc/not-found.md)에게 이 제스처로 인해 발생했던 지난번 액션 메서드 호출을 기준으로 그 이후의 회전각도\(라디안 단위\)를 요청하는 것이 가능합니다. 또한 제스처 인식기의 클라이언트는 [location\(in:\)](../../../etc/not-found.md)이나 [location\(ofTouch:in:\)](../../../etc/not-found.md)을 호출함으로써 제스처의 위치를 요청할 수도 있습니다.

제스처 인식기를 통해 해석되는 제스처는 연속적일 수도, 불연속적일 수도 있습니다. 더블 탭 같은 불연속 제스처는 여러번의 터치 시퀀스에도 불구하고 한번 발생하고 하나의 액션만 전송됩니다. 하지만 회전 제스처와 같이 연속적인 제스처를 해석하는 경우에는 멀티 터치 시퀀스가 끝날때까지 각 변화에 대한 액션 메세지를 계속해서 보냅니다.

window는 터치 이벤트를 제스처 인식기에 연결된 hit-test 된 뷰로 전달하기 전에 제스처 인식기에 먼저 전달합니다. 일반적으로 제스처 인식기는 터치 스트림을 멀티 터치 시퀀스로 분석하고 제스처를 인식하지 못하면 뷰는 터치 전체의 보완을 받습니다. 제스처 인식기가 제스처를 인식하면 에 대한 나머지 터치는 취소됩니다. 제스처 인식의 일반적인 동작 시퀀스는 [cancelsTouchesInView](../../../etc/not-found.md), [delaysTouchesBegan](../../../etc/not-found.md), [delaysTouchesEnded](../../../etc/not-found.md) 프로퍼티의 기본값에 따라 결정됩니다:

* cancelsTouchesInView—제스처 인식기가 제스처를 인식하면 제스처 인식기는 해당 제스처의 나머지 터치들을 뷰로부터 바인딩 해제합니다. \(이에 따라 window는 나머지 터치들을 전달하지 않습니다.\) window는 이전에 전달한 터치를 touchesCancelled\(\_:with:\) 메세지로 취소합니다. 만약 제스처 인식기가 제스처를 인식하지 못하면 뷰는 모든 터치를 멀티터치 시퀀스로 받습니다.
* delaysTouchesBegan—터치 이벤트를 분석할 때 제스처의 인식에 실패하지 않는 한 window는 연결된 뷰에 UITouch.Phase.began 상태의 터치 객체를 전달하는 것을 보류합니다. 제스처 인식기가 이어서 제스처를 인식하면 뷰는 이들 터치 객체를 받지 않습니다. 만약 제스처 인식기가 제스처를 인식하지 못하면 window는 이들 객체를 뷰의 touchesBegan\(:with:\) 메서드 호출시 전달합니다. \(가능한 경우 후속 메서드인 touchesMoved\(:with:\)가 현재 터치 위치를 알려줍니다.\)
* delaysTouchesEnded—터치 이벤트를 분석할 때 제스처의 인식에 실패하지 않는 한 window는 연결된 뷰에 UITouch.Phase.ended 상태의 터치 객체를 전달하는 것을 보류합니다. 제스처 인식기가 이어서 제스처를 인식하면 보류된 터치들은 취소됩니다. \(touchesCancelled\(:with:\) 메세지로 전달됩니다.\) 만약 제스처 인식기가 제스처를 인식하지 못하면 window는 터치 객체를 뷰의 touchesEnded\(:with:\) 메서드 호출시에 전달합니다.

위 설명에서의 "인식"은 반드시 인식 상태의 전환이라는 의미와 동일하지는 않습니다.

### Subclassing Notes

"check mark" 같은 독특한 제스처를 인식하기 위해서 UIGestureRecognizer의 서브클래스를 생성할 일이 생길 수 있습니다. 이러한 구상 제스처 인식기를 만들고자 한다면 UIGestureRecognizerSubclass.h 헤더 파일을 import 하세요. 이 헤더 파일은 서브클래스가 오버라이드, 호출 또는 재설정해야 하는 모든 메서드 및 프로퍼티를 선업합니다. 제스처 인식기는 사전 정의된 상태 시스템 내에서 동작하여 멀티 터치 이벤트를 터치할 때 후속 상태로 전환합니다. 제스처가 연속형인지 불연속형인지에 따라서 상태와 가능한 전환 동작이 달라집니다. 모든 제스처 인식기는 Possible 상태\([UIGestureRecognizer.State.possible](../../../etc/not-found.md)\)에서부터 멀티 터치 시퀀스를 시작합니다. 불연속 제스처는 Possible에서 시작하여 제스처가 성공적으로 해석되면 Recognized \([recognized](../../../etc/not-found.md)\), 그렇지 않으면 Failed \([UIGestureRecognizer.State.failed](../../../etc/not-found.md)\)로 전환됩니다. 제스처 인식기가 Recognized로 전환되면 동작 메세지를 타겟에 전달합니다.

연속 제스처의 경우 다음과 같이 더 많은 상태전환이 가능합니다:

* Possible ----&gt; Began ----&gt; \[Changed\] ----&gt; Cancelled
* Possible ----&gt; Began ----&gt; \[Changed\] ----&gt; Ended

Changed 상태는 선택적이지만 Cancelled나 Ended에 도달하기 이전에 여러번 발생할 수 있습니다. 따라서 핀치\(pinch\)와 같은 연속적인 제스처의 경우 두 손가락이 가까워지거나 멀어질때마다 동작 메세지가 전송됩니다. 이런 상태를 나타내는 enum 상수는 UIGestureRecognizer.State 타입입니다. \(Recognized와 Ended 상태의 상수는 동의어입니다.\)

서브 클래스는 상태간 전이가 일어날 때 state 프로퍼티를 적절한 값으로 설정해야 합니다.

### 오버라이드 할 메서드 <a id="methods-to-override"></a>

 서브클래스들은 [서브클래스를 위한 메서드](uigesturerecognizer.md#methods-for-subclasses)를 반드시 오버라이드 해야 합니다. 또한 \(위에 설명된 대로\) [state](../../../etc/not-found.md) 프로퍼티를 주기적으로 재설정해주어야 하며 [ignore\(\_:for:\)](../../../etc/not-found.md) 메서드를 호출할 수도 있습니다.

### 특별 고려사항 <a id="special-considerations"></a>

[state](../../../etc/not-found.md) 프로퍼티는 UIGestureRecognizer.h에 읽기 전용으로 선언되어 있습니다. 이 프로퍼티 선언은 제스처 인식기의 클라이언트를 위한 것입니다. UIGestureRecognizer의 서브클래스는 반드시 UIGestureRecognizerSubclass.h를 import 해야 하며 이 헤더파일에는 state의 읽기-쓰기가 가능하게 해주는 재선언이 포함되어 있습니다.

## 주제 <a id="topics"></a>

### 제스처 인식기 초기화 <a id="initializing-a-gesture-recognizer"></a>

* init\(target: Any?, action: Selector?\) 할당된 제스처 인식기 객체를 타겟과 액션 셀렉터로 초기화합니다.

### 제스처 관련 상호작용 관리 <a id="managing-gesture-related-interactions"></a>

* _var_ delegate: UIGestureRecognizerDelegate?

  제스처 인식기의 delegate

* _protocol_ UIGestureRecognizerDelegate

  제스처 인식기의 delegate를 통해 구현되는 메서드 집합. 앱의 제스처 인식 동작을 세밀하게 조정합니다.

### 타겟/액션 추가 및 삭제 <a id="adding-and-removing-targets-and-actions"></a>

* _func_ addTarget\(Any, action: Selector\) 타겟과 액션을 제스처 인식기 객체에 추가합니다.
* _func_ removeTarget\(Any?, action: Selector?\) 타겟과 액션을 제스처 인식기 객체로부터 제거합니다.

### 터치 및 제스처의 위치 <a id="getting-the-touches-and-location-of-a-gesture"></a>

* _func_ location\(in: UIView?\) -&gt; CGPoint

  리시버가 나타내는 제스처를 주어진 뷰 안의 위치로 계산하여 반환합니다.

* _func_ location\(ofTouch: Int, in: UIView?\) -&gt; CGPoint 주어진 뷰의 로컬 좌표계에서 제스처 터치 중 하나의 위치를 반환합니다.
* _var_ numberOfTouches: Int 리시버가 나타내는 제스처에 포함된 터치의 갯수를 반환합니다.

### 인식기의 상태와 뷰 <a id="getting-the-recognizers-state-and-view"></a>

* _var_ state: UIGestureRecognizer.State

  제스처 인식기의 현재 상태

* _var_ view: UIView? 제스처 인식기가 연결된 뷰
* _var_ isEnabled: Bool 제스처 인식기의 활성화 여부를 나타내는 Boolean 프로퍼티

### 터치의 취소와 지연 <a id="canceling-and-delaying-touches"></a>

* _var_ cancelsTouchesInView: Bool 제스처가 인식될 때 터치를 뷰로 전달할 것인지를 나타내는 Boolean 값
* _var_ delaysTouchesBegan: Bool begin 상태일 때 리시버가 뷰로 보내는 터치의 전송을 지연시킬 것인지를 나타내는 Boolean 값
* _var_ delaysTouchesEnded: Bool end 상태일 때 리시버가 뷰로 보내는 터치의 전송을 지연시킬 것인지를 나타내는 Boolean 값

### 제스처 인식기 간 의존성 명시 <a id="specifying-dependencies-between-gesture-recognizers"></a>

* func require\(toFail: UIGestureRecognizer\) 객체가 생성될 때 리시버와 다른 제스처 인식기 사이에 의존 관계를 만듭니다.

### 다양한 제스처 인식 <a id="recognizing-different-gestures"></a>

* _var_ allowedPressTypes: \[NSNumber\]

  버튼 프레스 타입을 구분하기 위해 사용되는 프레스 타입의 배열

* _var_ allowedTouchTypes: \[NSNumber\] 터치 타입을 구분하기 위해 사용되는 터치 타입의 배열
* _var_ requiresExclusiveTouchType: Bool 제스처 인식기가 다른 타입의 터치를 동시에 인식하도록 할 것인지를 나타내는 Boolean

### 서브클래스를 위한 메서드 <a id="methods-for-subclasses"></a>

UIGestureRecognizerSubclass.h 헤더 파일에는 UIGestureRecognizer의 서브클래스를 통해서만 호출되거나 오버라이드되는 메서드를 선언하는 클래스 확장이 포함되어 있습니다. UIGestureRecognizer의 구상 서브클래스만을 사용하는 클라이언트는 \(명시된 것을 제외하고는\) 이 메서드들을 사용해서는 안됩니다.

* _func_ touchesBegan\(Set, with: UIEvent\) 연결된 뷰에 하나 이상의 손가락이 닿았을 때 제스처 인식기로 전송됩니다.
* _func_ touchesMoved\(Set, with: UIEvent\) 연결된 뷰에서 하나 이상의 손가락이 움직였을 때 제스처 인식기로 전송됩니다.
* _func_ touchesEnded\(Set, with: UIEvent\) 연결된 뷰에서 하나 이상의 손가락이 떨어졌을 때 제스처 인식기로 전송됩니다.
* _func_ touchesCancelled\(Set, with: UIEvent\) \(전화가 왔을 때와 같은\) 시스템 이벤트가 터치 이벤트를 취소할  때 제스처 인식기로 전송됩니다.
* _func_ touchesEstimatedPropertiesUpdated\(Set\) 터치의 예상 프로퍼티가 변경되어서 예측이 불가능하거나 더 이상의 업데이트가 예상되지 않을 때 제스처 인식기로 전송됩니다.
* _func_ reset\(\) 제스처 인식 시도가 완료되었을 때 내부 상태를 리셋하기 위해서 오버라이드 됩니다.
* _func_ ignore\(UITouch, for: UIEvent\) 제스처 인식기에 주어진 이벤트의 특정 터치를 무시하도록 지시합니다.
* _func_ canBePrevented\(by: UIGestureRecognizer\) -&gt; Bool 오버라이드를 통해 지정된 제스처 인식기가 리시버의 제스처 인식을 제한시킬 수 있음을 나타냅니다.
* _func_ canPrevent\(UIGestureRecognizer\) -&gt; Bool 오버라이드를 통해 리시버의 제스처 인식이 지정된 제스처 인식기를 제한시킬 수 있음을 나타냅니다.
* _func_ shouldRequireFailure\(of: UIGestureRecognizer\) -&gt; Bool 오버라이드를 통해 리시버가 지정된 제스처 인식기의 실패를 필요로 함을 나타냅니다.
* _func_ shouldBeRequiredToFail\(by: UIGestureRecognizer\) -&gt; Bool 오버라이드를 통해 지정된 제스처 인식기가 리시버의 실패를 필요로 함을 나타냅니다.
* _func_ ignore\(UIPress, for: UIPressesEvent\) 제스처 인식기에 주어진 이벤트의 특정 press를 무시하도록 지시합니다.
* _func_ pressesBegan\(Set, with: UIPressesEvent\) 연결된 뷰의 물리 버튼이 눌렸을 때 리시버로 전송합니다.
* _func_ pressesChanged\(Set, with: UIPressesEvent\) 연결된 뷰에서 누르는 압력이 변경되었을 때 리시버로 전송합니다.
* _func_ pressesEnded\(Set, with: UIPressesEvent\) 연결된 뷰에서 버튼을 놓았을 때 리시버로 전송합니다.
* _func_ pressesCancelled\(Set, with: UIPressesEvent\) \(메모리 부족 경고와 같은\) 시스템 이벤트가 press 이벤트를 취소할 때 리시버로 전송합니다.

### 제스처 인식기 디버깅 <a id="debugging-gesture-recognizers"></a>

* _var_ name: String? 제스처 인식와 관련된 이름

### 상수 <a id="constants"></a>

* _enum_ UIGestureRecognizer.State

  제스처 인식기의 현재 상태

### 이니셜라이저 <a id="initializers"></a>

* init\(\) `Beta`
* init?\(coder: NSCoder\) `Beta`

## 관련 문서 <a id="relationships"></a>

### 상속 <a id="inherits-from"></a>

* NSObject

### 준수하는 프로토콜 <a id="conforms-to"></a>

* CVarArg
* Equatable
* Hashable

## 같이 보기 <a id="see-also"></a>

### 커스텀 제스처 <a id="custom-gestures"></a>

* Implementing a Custom Gesture Recognizer 언제, 그리고 어떻게 제스처 인식기를 직접 빌드할 수 있는지 알아보세요.
* _protocol_ UIGestureRecognizerDelegate 제스처 인식기의 위임자에 의해서 구현되는 메서드들. 앱의 제스처 인식 동작을 정밀하게 조정합니다.

