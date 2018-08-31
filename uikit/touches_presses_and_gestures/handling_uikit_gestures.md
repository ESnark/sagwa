# UIKit 제스처 처리

> 원본출처  
> [https://developer.apple.com/documentation/uikit/touches\_presses\_and\_gestures/handling\_uikit\_gestures](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_uikit_gestures)

## 개요

제스처 인식기는 보기에서 터치 이벤트나 프레스 이벤트를 처리하는 가장 간단한 방법입니다. 하나 이상의 제스처 인식기를 모든 뷰에 연결 할 수 있습니다. 제스처 인식기는 해당 뷰에 대해 들어오는 이벤트를 처리, 해석하고 알려진 패턴과 매치시키는데 필요한 모든 로직을 캡슐화합니다. 일치하는 패턴을 발견하면 제스처 인식기는 할당된 target\(대상\) 객체에 알립니다. 대상 객체는 view controller나 view, 또는 앱 상의 다른 객체일수도 있습니다.

제스처 인식기는 알림을 보내는데 target-action 디자인 패턴을 사용합니다. [UITabGestureRecognizer](../../not-found.md) 객체가 뷰에서 한 손가락 탭을 감지하면 해당 객체는 그 뷰의 뷰 컨트롤러에서 \(응답을 제공하기 위한\) Action 메서드를 호출합니다.

![&#xADF8;&#xB9BC; 1. &#xD0C0;&#xAC9F;&#xC5D0; &#xC54C;&#xB9BC;&#xC744; &#xBCF4;&#xB0B4;&#xB294; &#xC81C;&#xC2A4;&#xCC98; &#xC778;&#xC2DD;&#xAE30;](https://docs-assets.developer.apple.com/published/7c21d852b9/0c8c5e29-c846-4a16-988b-3d809eafbb6b.png)

제스처 인식기는 이산형과 연속형의 두 가지 타입이 있습니다. **이산 제스처 인식기**는 제스처가 인식된 후 정확히 한 번 Action 메서드를 호출합니다. 초기 인식 기준을 충족하면 **연속 제스처 인식기**가 Action 메서드를 여러번 호출하여 제스처 이벤트의 정보가 변경될 때마다 알려줍니다. 예를 들어 [UIPanGestureRecognizer](../../not-found.md) 객체는 터치 위치가 변경될 때마다 Action 메서드를 호출합니다.

Interface Builder에는 표준 UIKit 제스처 인식기 각각에 대한 객체가 포함되어 있습니다. 또한 커스텀 [UIGestureRecognizer](../../not-found.md) 서브클래스를 나타내는데 사용할 수 있는 커스텀 제스처 인식기 객체도 포함됩니다.

## 제스처 인식기 설정하기

제스처 인식기를 설정하기 위해서는 다음 단계를 따라야 합니다:

1. 스토리보드에서 제스처 인식기를 뷰에 끌어다 놓으세요.
2. 제스처가 인식되었을 때 호출될 Action 메서드를 구현하세요.
3. Action 메서드와 제스처 인식기를 연결합니다.

Interface Builder에서 제스처 인식기를 마우스 오른쪽 버튼으로 클릭하고 Sent Action Selector를 인터페이스의 적절한 객체에 연결하여 연결을 구성할 수 있습니다. 제스처 인식기의 [addTarget \(\_ : action :\)](../../not-found.md) 메서드를 사용하여 프로그래밍 방식으로 Action 메서드를 구성할 수도 있습니다.

Listing 1은 제스처 인식기의 Action 메서드에 대한 일반적인 형식을 보여줍니다. 원하는 경우 특정 제스처 인식기 하위 클래스와 일치하도록 파라미터 유형을 변경할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="Listing 1 제스처 인식기 Action 메서드" %}
```swift
@IBAction func myActionMethod(_ sender: UIGestureRecognizer)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 제스처에 응답하기

제스처 인식기와 연결된 Action 메서드는 해당 제스처에 대한 앱의 응답을 제공합니다. 이산 제스처의 경우 Action 메서드는 버튼의 Action 메서드와 비슷합니다. Action 메서드가 호출되면 해당 제스처에 적합한 작업을 수행합니다. 연속 제스의 경우 Action 메서드는 인식된 제스처에 응답할 수도 있지만 제스처가 인식되기 전에 이벤트를 추적할 수도 있습니다. 이벤트 추적은 더 많은 상호작용 경험을 가능하게 합니다. 예를 들어, [UIPanGestureRecognizer](../../not-found.md) 객체로부터의 업데이트를 사용하여 앱의 컨텐츠 위치를 변경할 수 있습니다.

제스처 인식기의 상태\(state\) 프로퍼티 객체의 현재 인식 상태를 전달합니다. 연속 제스처의 경우 제스처 인식기는 이 프로퍼티를 [UIGestureRecognizer.State.began](../../not-found.md)에서 [UIGestureRecognizer.State.changed](../../not-found.md)와[UIGestureRecognizer.State.ended](../../not-found.md)로 또는 [UIGestureRecognizer.State.cancelled](../../not-found.md)로 업데이트합니다. Action 메서드는 이 프로퍼티를 사용하여 적절한 action 과정을 판별합니다.  
예를 들어 시작 상태와 변경된 상태를 사용하여 컨텐츠를 일시적으로 변경하고 종료 상태를 사용하여 변경 사항을 영구적으로 유지한 다음 취소된 상태를 사용하여 변경 사항을 취소할 수 있습니다. 동작을 취하기 전에 제스처 인식기의 상태 프로퍼티를 항상 확인하세요.

특정 유형의 제스처를 처리하는 방법에 대한 예시는 다음 정보를 참조하세요:

* 탭 제스처 처리하기
* 길게 누르는 제스처 처리하기
* Pan 제스처 처리하기
* 스와이프 제스처 처리하기
* Pinch 제스처 처리하기
* 회전 제스처 처리하기

제스처 인식기 상태와 해당 상태가 코드에 미치는 영향에 대한 자세한 내용은 [커스텀 제스처 인식 구현을](../../not-found.md) 참조하세요

## 제스처

* 탭 제스처 처리하기 화면에서 간단한 탭을 사용하여 컨텐츠에 버튼과 유사한 상호작용을 구현합니다.
* 길게 누르는 제스처 처리하기 화면에서 오랫동안 누르는 탭을 감지하고 이를 사용하여 상황별로 관련 컨텐츠를 표시합니다.
* Pan 제스처 처리하기 화면에서 손가락의 움직임을 추적하고 해당 동작을 컨텐츠에 적용합니다.
* 스와이프 제스처 처리하기 화면에서 수평 또는 수직 스와이프 동작을 감지하고 이 동작을 사용하여 컨텐츠를 탐색합니다.
* Pinch 제스처 처리하기 두 손가락 사이의 거리를 추적하고 해당 정보를 사용하여 컨텐츠를 확대/축소합니다.
* 회전 제스처 처리하기 화면에서 두 손가락의 상대적인 회전을 측정하고 그 동작을 사용하여 컨텐츠를 회전합니다.

## 같이 보기

### UIKit 제스처

* [다중 제스처 인식기 조정](../../not-found.md) 동일한 뷰에서 여러 개의 제스처 인식기를 사용하는 방법을 확인합니다.
* class UILongPressGestureRecognizer 길게 누르기 제스처를 인식하는 [UIGestureRecognizer](../../not-found.md)의 구상 하위 클래스
* class UIPanGestureRecognizer 패닝\(드래그\) 제스처를 인식하는 [UIGestureRecognizer](../../not-found.md)의 구상 하위 클래스
* class UIPinchGestureRecognizer 두 개의 터치로 꼬집는 제스처를 인식하는 [UIGestureRecognizer](../../not-found.md)의 구상 하위 클래스
* class UIScreenEdgePanGestureRecognizer 화면 가장자리 근처에서 시작하는 패닝\(드래그\) 제스처를 인식하는 제스처 인식기
* class UISwipeGestureRecognizer 하나 이상의 방향으로 스와이프하는 제스처를 인식하는 [UIGestureRecognizer](../../not-found.md)의 구상 하위 클래스
* class UIRotationGestureRecognizer 두 개의 터치로 회전하는 제스처를 인식하는 [UIGestureRecognizer](../../not-found.md)의 구상 하위 클래스
* class UITapGestureRecognizer 싱글탭이나 멀티탭을 인식하는 [UIGestureRecognizer](../../not-found.md)의 구상 하위 클래스

