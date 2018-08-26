---
description: 화면상의 직사각형 영역에 대한 컨텐츠를 관리하는 개체입니다.
---

# UIView

> 원본출처  
> [https://developer.apple.com/documentation/uikit/uiview](https://developer.apple.com/documentation/uikit/uiview)

## 개요

뷰는 앱 사용자 인터페이스의 기본 구성요소이며 UIView 클래스는 모든 뷰에 공통 동작을 정의합니다. 뷰 객체는 사각형 경계 내에 컨텐츠를 렌더링하고 해당 컨텐츠와의 상호작용을 처리합니다. UIView 클래스는 초기화하여 고정된 배경색을 표시하는데 사용될 수 있는 구상 클래스입니다. 보다 정교한 컨텐츠를 그리기 위해서 서브클래스화할 수도 있습니다.  
앱에서 흔히 볼 수있는 라벨, 이미지, 버튼 및 기타 인터페이스 요소를 표시하려면 직접 정의하기보다는 UIKit 프레임워크에서 제공하는 뷰 하위 클래스를 사용하세요.

뷰 객체는 앱이 사용자와 상호작용하는 주된 방식이기 때문에 여러 가지 임무가 있습니다. 다음은 몇 가지 예입니다:

* 그리기와 애니메이션
  * 뷰는 자신의 사각형 영역 안에서 UIKit이나 Core Graphics를 사용하여 컨텐츠를 그려냅니다.
  * 어떤 뷰 프로퍼티들은 새로운 값으로 애니메이션 될 수 있습니다.
* 레이아웃과 서브 뷰 관리
  * 뷰는 0개 이상의 서브뷰를 가질 수 있습니다.
  * 뷰는 서브뷰의 크기와 위치를 조정할 수 있습니다.
  * 뷰 계층구조의 변화에 대응할 수 있도록 자동 레이아웃을 사용해서 뷰의 크기와 위치를 재조정하는 규칙을 만드세요.
* 이벤트 처리
  * 뷰는 UIResponder의 하위 클래스이기 때문에 터치나 기타 다른 이벤트에 응답할 수 있습니다.
  * 뷰에는 일반 제스처를 처리하는 제스처 인식기가 설치될 수 있습니다.

뷰는 다른 뷰 내부에 중첩되어 뷰 계층을 만들 수 있으므로 관련 컨텐츠를 편리하게 구성할 수 있습니다. 뷰를 중첩하면 중첩된 하위 뷰와 상위 뷰 사이에 상하위 관계가 만들어집니다. 상위 뷰에는 여러 개의 하위 뷰가 포함될 수 있지만 각 하위 뷰에는 하나의 슈퍼 뷰만 있습니다. 기본적으로 하위 뷰의 보이는 영역이 수퍼 뷰의 범위를 벗어나 확장되어도 하위 뷰의 내용이 잘리지 않습니다. 해당 동작 방식을 변경하려면 clipsToBounds 속성을 사용하세요.

각 뷰의 범위는 그 frame과 경계\(bounds\) 속성에 의해 결정됩니다. frame 속성은 수퍼 뷰 좌표계의 안에서 원점과 크기로 정해집니다. bounds 속성은 뷰의 내부적인 수치를 의미하며 커스텀 그리기 코드 내에서 배타적으로 사용됩니다. center 속성을 사용하면 frame이나 bounds 특성을 직접 변경하지 않고도 뷰의 위치를 쉽게 변경할 수 있습니다.

UIView 클래스를 사용하는 방법에 대한 자세한 내용은 [iOS용 View 프로그래밍 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하세요

## 뷰 생성하기

일반적으로 스토리보드에 뷰를 만들때는 라이브러리로부터 캔버스에 끌어다 놓아서 만들지만 프로그래밍적인 방법으로도 생성할 수 있습니다. 뷰를 생성할 때에는 대개 미래의 수퍼 뷰와 관련된 초기 크기와 위치를 지정합니다. 예를 들어 다음 예제에서는 뷰를 작성하고 Superview의 좌표계에 있는 점\(10, 10\)에 왼쪽 상단 모서리를 배치합니다.

```swift
let rect = CGRect(x: 10, y: 10, width: 100, height: 100)
let myView = UIView(frame: rect)
```

다른 뷰에 하위 뷰를 추가하려면 수퍼 뷰에서 [addSubview \(\_ :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 호출하세요. 뷰에 하위 뷰를 여러 개 추가할 수 있으며, 형제 뷰는 iOS에서 아무 문제없이 서로 겹칠 수 있습니다. addSubview \(\_ :\) 메소드를 호출 할 때마다 새 뷰가 다른 기존 형제 뷰 위에 놓입니다. [insertSubview \(\_ : aboveSubview :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 및 [insertSubview \(\_ : belowSubview :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 사용하여 하위 뷰의 상대 z 순서를 지정할 수 있습니다. [exchangeSubview \(at : withSubviewAt :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 사용하여 이미 추가 된 하위 뷰의 위치를 ​​교환할 수도 있습니다.

뷰를 생성한 후 자동 레이아웃 규칙을 작성하여 나머지 뷰 계층 구조의 변화에 따라 뷰의 크기와 위치가 변경되는 방법을 제어할 수 있습니다. 자세한 내용은 [자동 레이아웃 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하세요.

## 뷰 드로잉 사이클

뷰 그리기는 기본적으로 필요에 따라 발생합니다. 뷰가 처음 표시되거나 레이아웃 변경으로 인해 전체나 일부가 표시되면 시스템은 뷰에 컨텐츠를 그려달라고 요청합니다.  
UIKit 또는 Core Graphics가 사용된 커스텀 컨텐츠가 포함된 뷰의 경우 시스템은 뷰의 draw \(\_ :\) 메서드를 호출하느데 이 메서드는 그래픽 컨텍스트에 뷰 컨텐츠를 그리는 방식으로 구현됩니다. \(그래픽 컨텍스트는 메서드 실행 전에 시스템이 자동적으로 설정하게 됩니다.\)  
이렇게 함으로써 뷰 컨텐츠가 화면상에 시각적으로 나타납니다.

뷰의 컨텐츠가 변경되면 다시 그려져야 한다고 시스템에 알리는 것은 개발자의 책임입니다. 뷰의 [setNeedsDisplay\(\)](https://melodyarchive.gitbook.io/sagwa/not-found) 또는 [setNeedsDisplay\(\_ :\)](https://melodyarchive.gitbook.io/sagwa/not-found) 메서드를 호출하여 작업을 수행할 수 있습니다.이 메서드는 다음 드로잉 사이클동안 뷰를 업데이트해야 한다고 시스템에 알립니다.  
뷰가 업데이트되는 것은 다음 드로잉 사이클까지 기다려야 하는 일이기 때문에 여러 뷰에서 이 메서드를 호출하고 동시에 업데이트 하는 것이 가능합니다.

{% hint style="info" %}
알림

OpenGL ES를 사용하여 그리는 경우 UIView의 하위 클래스 대신 [GLKView](https://melodyarchive.gitbook.io/sagwa/not-found) 클래스를 사용해야 합니다. OpenGL ES를 사용하여 그리는 방법에 대한 자세한 내용은 [OpenGL ES 프로그래밍 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하십시오.
{% endhint %}

뷰 드로잉 사이클과 이 사이클에서 뷰가 맡는 역할에 대한 더 자세한 정보는 [iOS용 View 프로그래밍 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하세요.

## 애니메이션 {#animations}

뷰 프로퍼티의 변동사항들은 애니메이션화 할 수 있습니다. 즉, 프로퍼티의 현재 값에서 시작해서 새로 지정한 값으로 끝나는 애니메이션이 생성됩니다. UIView 클래스의 프로퍼티 중에서 애니메이션에 적합한 것들은 다음과 같습니다:

* frame
* bounds
* center
* transform
* alpha
* backgroundColor

변경사항을 애니메이션화하려면 [UIViewPropertyAnimator](https://melodyarchive.gitbook.io/sagwa/not-found) 객체를 만들고 객체의 핸들러 블럭을 사용하여 뷰 프로퍼티를 변경합니다. UIViewPropertyAnimator의 클래스 메서드를 사용하여 애니메이션의 지속시간이나 타이밍을 설정할 수 있지만 이 경우에는 애니메이션이 그 즉시 실행됩니다. 또한 프로퍼티 기반 애니메이터는 실행 중에 멈추거나 대화형으로 구동될 수 있습니다.  
자세한 내용은 [UIViewPropertyAnimator](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하세요.

## 스레딩 고려사항

앱의 유저 인터페이스를 조작할때에는 반드시 메인 스레드에서 작업해야 합니다. 그러므로 UIView 클래스의 메서드를 호출하는 코드도 반드시 메인 스레드에서 동작해야 합니다. 이 규칙에서 비교적 자유로운 단 한가지 예외는 뷰 객체를 생성하는 경우 뿐입니다. 그 외에는 반드시 메인 스레드에서만 작업하세요

## Subclassing Notes

UIView 클래스는 시각적 컨텐츠와 더불어 유저 상호작용 제공을 위한 중요한 서브클래싱 지점입니다. UIView를 서브클래싱해야 할 이유야 많겠지만 상속은 기본 UIView 클래스나 표준 시스템 뷰가 필요한 기능을 제공하지 못할 때 하는 것을 권장합니다. 서브클래싱을 사용하면 뷰를 구현하고 성능을 최적화하는데 더 많은 작업이 필요합니다.

서브클래싱을 피하는 방법에 대한 정보는 [서브클래싱의 대안](https://melodyarchive.gitbook.io/sagwa/not-found)을 참조하세요

### 오버라이드할 메서드

UIView를 서브클래싱할 때 반드시 오버라이드 해야하는 메서드는 몇 없고 대다수는 필요에 따라서만 하면 됩니다. UIView는 상당히 유연하게 설정 가능한 클래스이기 때문에 커스텀 메서드를 오버라이드하지 않고도 정교한 뷰 동작을 구현할 수 있는 방법들이 많이 있습니다. 그 방법들은 [서브클래싱의 대안](https://melodyarchive.gitbook.io/sagwa/uikit/view_and_controls/uiview#alternatives_to_subclassing) 섹션에서 논의하도록 하고 여기서는 UIView의 하위 클래스에서 오버라이드 할 수 있는 메서드를 보겠습니다:

* 초기화
  * init\(frame:\) - 이 메서드는 구현하는 것이 권장됩니다. 커스텀 메서드를 추가구현하거나 아예 대체하는 메서드를 구현하는 것 또한 가능합니다.
  * init\(coder:\) - 스토리보드나 nib 파일에서 커스텀 초기화가 필요한 뷰를 불러오는 경우 이 메서드를 구현하세요.
  * [layerClass](https://melodyarchive.gitbook.io/sagwa/not-found) 이 프로퍼티는 백업 저장소에서 뷰가 다른 Core Animation 레이어를 사용하게 하려는 경우에 사용하세요. 예를 들어 하나의 뷰를 스크롤 가능한 넓은 영역에 타일방식으로 디스플레이하고자 한다면 이 프로퍼티를 [CATiledLayer](https://melodyarchive.gitbook.io/sagwa/not-found) 클래스로 설정하는 것이 좋습니다.
* 드로잉과 프린팅
  * draw\(\_:\) - 뷰가 커스텀 컨텐츠를 그리는 경우 이 메서드를 구현하세요. 뷰가 커스텀 드로잉을 수행하는 경우가 아니라면 이 메서드는 오버라이드하지 않는 것이 좋습니다.
  * draw\(\_:for:\) - 프린팅 중에 뷰를 다르게 그리고자 하는 경우에만 이 메서드를 구현하세요.
* 레이아웃과 제약조건
  * [requiresConstraintBasedLayout](https://melodyarchive.gitbook.io/sagwa/not-found)  뷰 클래스가 제대로 동작하기 위해서 제약조건을 필요로 하는 경우 이 프로퍼티를 사용하세요.
  * updateConstraints\(\) - 뷰와 하위 뷰 간에 커스텀 제약조건을 작성해야 하는 경우 이 메서드를 구현하세요
  * alignmentRect\(forFrame:\), frame\(forAlignmentRect:\) - 뷰와 다른 뷰 간의 정렬방법을 오버라이드하려면 이 메서드들을 구현하세요.
  * didAddSubview\(\_:\), willRemoveSubview\(\_:\) - 하위 뷰의 생성과 제거를 추적해야 할 필요가 있다면 이 메서드들을 구현하세요.
  * willMove\(toSuperview:\), didMoveToSuperview\(\) - 현재 뷰가 뷰 계층간에 이동하는 것을 추적하고 싶다면 이 메서드들을 구현하세요.
* 이벤트 핸들링
  * gestureRecognizerShouldBegin\(\_:\) - 뷰가 터치 이벤트를 직접 처리하는 동시에 연결된 제스처 인식기가 다른 작업을 트리거하지 못하도록 하려면 이 메서드를 구현하세요.
  * touchesBegan\(\_:with:\), touchesMoved\(\_:with:\), touchesEnded\(\_:with:\), touchesCancelled\(\_:with:\) - 터치 이벤트를 직접 처리하고 싶다면 이 메서드를 구현하세요.\(제스처 기반 입력을 처리하고 싶으면 제스처 인식기를 사용하세요\)

### 서브클래싱의 대안

서브클래싱을 하지 않고도 많은 뷰 동작이 설정가능합니다. 원하는 동작을 제공하기 위해서 메서드를 오버라이드 하기 전에 다음 프로퍼티나 동작을 수정하는 것을 고려해보세요.

* addConstraint\(\_:\) - 뷰와 하위 뷰를 위한 자동 레이아웃 동작을 설정하세요.
* autoresizingMask - 상위 뷰 프레임에 변동이 있을때 자동 레이아웃 동작을 제공합니다. 이 동작은 제약사항과 결합될 수 있습니다.
* contentMode - 뷰 프레임이 아닌 뷰 컨텐츠에 대한 레이아웃 동작을 제공합니다. 또한 이 프로퍼티는 뷰에 맞게 컨텐츠를 조정하는 방법을 제공하고 컨텐츠를 새로 그릴지 캐시할지 결정할 수 있습니다.
* isHidden or alpha - 뷰 내에서 렌더링된 개별 컨텐츠의 알파값을 조정하거나 숨기는 대신에 뷰 전체의 투명도를 조정할 수 있습니다.
* backgroundColor - 색을 직접 그리는 대신에 뷰의 색상을 설정합니다.
* Subviews - draw\(\_:\) 메서드를 사용해서 컨텐츠를 그리는 대신 이미지와 label을 표시할 컨텐츠와 함께 포함시키세요.
* Gesture recognizers - 터치 이벤트를 가로채서 직접 처리하는 서브클래스를 만드는 대신에 제스처 인식기를 사용하여 대상 객체에 액션을 보낼 수 있습니다.
* Animations - 애니메이션 동작을 직접 만드는 대신 내장 애니메이션 지원기능을 사용할 수 있습니다. Core Animation에 의해서 동작하는 애니메이션 지원기능은 빠르고 사용하기 쉽습니다.
* Image-based backgrounds - 상대적으로 정적인 컨텐츠를 표시하는 뷰에는 서브클래싱을 이용해서 직접 이미지를 그리기보다 UIImageView 객체와 제스처 인식기를 사용하는 것이 좋을 수 있습니다. 또는 일반 UIView 객체를 사용하고 이미지를 뷰의 CALayer 컨텐츠로 지정할수도 있습니다.

애니메이션은 복잡한 드로잉 코드의 서브클래싱과 구현없이 시각적 변화를 줄 수 있는 또 다른 방법입니다.  
UIView 클래스의 많은 프로퍼티들이 애니메이션 가능하며 이러한 프로퍼티의 변경으로 시스템에서 생성된 애니메이션이 트리거될 수 있습니다. 애니메이션을 시작하려면 뒤따르는 변경사항을 애니메이션으로 표현해야 한다는 코드 한 줄만 있으면 됩니다. 뷰의 애니메이션 지원에 대한 자세한 내용은 [애니메이션](https://melodyarchive.gitbook.io/sagwa/uikit/view_and_controls/uiview#animation)을 참조하세요.

## 주제

### 뷰 객체 생성하기

* init\(frame: CGRect\) 지정된 프레임 사각을 사용하여 새로 할당된 뷰 객체를 초기화하고 반환합니다.
* init?\(coder: NSCoder\)

### 뷰의 모양 설정하기

* _var_ backgroundColor: UIColor? 뷰의 배경색
* _var_ isHidden: Bool 뷰의 숨김상태를 결정하는 Boolean 값
* _var_ alpha: CGFloat 뷰의 알파값
* _var_ isOpaque: Bool 뷰의 불투명 상태를 결정하는 Boolean 값
* _var_ tintColor: UIColor! The first nondefault tint color value in the view’s hierarchy, ascending from and starting with the view itself.
* _var_ tintAdjustmentMode: UIViewTintAdjustmentMode The first non-default tint adjustment mode value in the view’s hierarchy, ascending from and starting with the view itself.
* _var_ clipsToBounds: Bool 하위 뷰를 뷰의 경계로 제한할지 여부를 결정하는 Boolean 값
* _var_ clearsContextBeforeDrawing: Bool 그리기 전에 뷰의 경계를 자동으로 지워야하는지 여부를 결정하는 Boolean 값
* _var_ mask: UIView? 알파 채널이 뷰의 내용을 마스킹하는 데 사용되는 선택적 뷰
* _class var_ layerClass: AnyClass 이 클래스의 인스턴스 레이어를 생성하는 데 사용되는 클래스를 반환합니다.
* _var_ layer: CALayer 렌더링에 사용되는 뷰의 Core Animation 레이어

### 이벤트 관련동작 설정하기

* _var_ isUserInteractionEnabled: Bool 사용자 이벤트를 무시하고 이벤트 큐에서 제거할지 결정하는 Boolean 값
* _var_ isMultipleTouchEnabled: Bool 뷰가 한 번에 두 개 이상의 터치를 받을 수 있도록 결정하는 Boolean 값
* _var_ isExclusiveTouch: Bool 수신자가 터치이벤트를 독점적으로 처리하도록 할지 결정하는 Boolean 값

### 경계\(Bounds\)와 프레임 사각형 설정하기

* _var_ frame: CGRect 상위 뷰 좌표계에서 뷰의 위치와 크기를 설명하는 프레임 사각형
* _var_ bounds: CGRect 자체 좌표계 내에서 뷰의 위치와 크기를 설명하는 경계 사각형
* _var_ center: CGPoint 뷰 프레임 사각형의 중심점
* _var_ transform: CGAffineTransform 경계 중심에 상대적인 뷰에 적용되는 변환을 지정합니다.

### 뷰 계층구조 관리하기

* _var_ superview: UIView? 수신자의 수퍼뷰. 없는 경우에는 nil
* _var_ subviews: \[UIView\] 수신자의 바로 아래 하위뷰
* _var_ window: UIWindow? 수신자의 window 객체. 없는 경우에는 nil
* _func_ addSubview\(UIView\) 수신자의 하위 뷰 리스트 끝에 뷰를 추가합니다.
* _func_ bringSubview\(toFront: UIView\) 지정된 하위 뷰를 이동시켜서 형제 뷰 위에 표시합니다.
* _func_ sendSubview\(toBack: UIView\) 지정된 하위 뷰를 이동시켜서 형제 뷰 아래에 표시합니다.
* _func_ removeFromSuperview\(\) 뷰를 상위 뷰와 window로부터 해제하고 응답자 체인으로부터 제거합니다.
* _func_ insertSubview\(UIView, at: Int\) 지정된 인덱스에 하위 뷰를 삽입합니다.
* _func_ insertSubview\(UIView, aboveSubview: UIView\) 뷰 계층상의 다른 뷰 위에 뷰를 삽입합니다.
* _func_ insertSubview\(UIView, belowSubview: UIView\) 뷰 계층상의 다른 뷰 아래에 뷰를 삽입합니다.
* _func_ exchangeSubview\(at: Int, withSubviewAt: Int\) 지정된 인덱스의 하위 뷰를 서로 교환합니다.
* _func_ isDescendant\(of: UIView\) 수신자가 주어진 뷰와 동일한 뷰거나 하위 뷰인지를 나타내는 Boolean 값을 반환합니다.

### 뷰 관련 변동사항 관찰하기

* _func_ didAddSubview\(UIView\) 하위 뷰가 추가되었음을 뷰에 알립니다.
* _func_ willRemoveSubview\(UIView\) 하위 뷰가 곧 삭제된다는 것을 뷰에 알립니다.
* _func_ willMove\(toSuperview: UIView?\) 상위 뷰가 지정된 다른 상위 뷰로 곧 바뀐다는 것을 뷰에 알립니다.
* _func_ didMoveToSuperview\(\) 상위 뷰가 바뀌었음을 뷰에 알립니다.
* _func_ willMove\(toWindow: UIWindow?\) window 객체가 곧 바뀐다는 것을 뷰에 알립니다.
* _func_ didMoveToWindow\(\) window 객체가 바뀌었음을 뷰에 알립니다.

### 컨텐츠 여백 설정하기

* [레이아웃 여백 범위 내에서 컨텐츠 배치하기](https://melodyarchive.gitbook.io/sagwa/not-found) 다른 view의 컨텐츠 때문에 view가 혼잡해지지 않도록 배치하세요.
* _var_ directionalLayoutMargins: NSDirectionalEdgeInsets 현재 언어 방향을 고려하여 뷰에서 컨텐츠를 배치할 때 사용할 기본 간격
* _var_ layoutMargins: UIEdgeInsets 뷰에 컨텐츠를 배치할 때 사용할 기본 간격
* _var_ preservesSuperviewLayoutMargins: Bool 현재 뷰가 상위 뷰의 여백도 준수할 것인지를 나타내는 Boolean 값
* _func_ layoutMarginsDidChange\(\) 레이아웃 여백이 변경되었음을 뷰에 알립니다.

### Safe Area 얻기

* [Safe Area에 상대적인 컨텐츠 위치 지정](https://melodyarchive.gitbook.io/sagwa/not-found) view가 다른 컨텐츠에 가려지지 않도록 배치하기.
* _var_ safeAreaInsets: UIEdgeInsets 이 뷰의 Safe Area를 결정하는데 사용되는 inset
* _var_ safeAreaLayoutGuide: UILayoutGuide 바 또는 기타 컨텐츠에 의해 가려지지 않는 뷰 영역을 나타내는 레이아웃 가이드
* _func_ safeAreaInsetsDidChange\(\) 뷰의 Safe Area가 변경되었을 때 호출됩니다.
* _var_ insetsLayoutMarginsFromSafeArea: Bool 뷰의 레이아웃 여백이 Safe Area를 반영하도록 자동적으로 업데이트할지를 나타내는 Boolean 값

### 뷰 제약사항 관리하기

자동 레이아웃 제약조건을 사용해서 뷰의 크기와 위치를 조정합니다.

* _var_ constraints: \[NSLayoutConstraint\] 뷰가 보유하는 제약조건
* _func_ addConstraint\(NSLayoutConstraint\) 수신자 뷰 또는 하위 뷰의 레이아웃에 제약조건을 추가합니다.
* _func_ addConstraints\(\[NSLayoutConstraint\]\) 수신자 뷰 또는 하위 뷰의 레이아웃에 여러 개의 제약조건을 추가합니다.
* _func_ removeConstraint\(NSLayoutConstraint\) 뷰로부터 지정된 제약조건을 제거합니다.
* _func_ removeConstraints\(\[NSLayoutConstraint\]\)

  뷰로부터 여러개의 제약조건을 제거합니다.

### 레이아웃 앵커를 사용해서 제약조건 만들기

뷰 앵커중 하나에 자동 레이아웃 조건을 추가합니다.

* _var_ bottomAnchor: NSLayoutYAxisAnchor 뷰 프레임의 하단 모서리를 나타내는 레이아웃 앵커
* _var_ centerXAnchor: NSLayoutXAxisAnchor 뷰 프레임의 수평 중심을 나타내는 레이아웃 앵커
* _var_ centerYAnchor: NSLayoutYAxisAnchor 뷰 프레임의 수직 중심을 나타내는 레이아웃 앵커
* _var_ firstBaselineAnchor: NSLayoutYAxisAnchor 뷰 가장 위 텍스트 라인에 대한 기준선을 나타내는 레이아웃 앵커
* _var_ heightAnchor: NSLayoutDimension 뷰 프레임의 높이를 나타내는 레이아웃 
* _var_ lastBaselineAnchor: NSLayoutYAxisAnchor 뷰 가장 아래 텍스트 라인에 대한 기준선을 나타내는 레이아웃 
* _var_ leadingAnchor: NSLayoutXAxisAnchor 뷰 프레임의 선행 가장자리를 나타내는 레이아웃 앵커
* _var_ leftAnchor: NSLayoutXAxisAnchor 뷰 프레임의 왼쪽 모서리를 나타내는 레이아웃 앵커
* _var_ rightAnchor: NSLayoutXAxisAnchor 뷰 프레임의 오른쪽 모서리를 나타내는 레이아웃 앵커
* _var_ topAnchor: NSLayoutYAxisAnchor 뷰 프래임의 상단 모서리를 나타내는 레이아웃 앵커
* _var_ trailingAnchor: NSLayoutXAxisAnchor 뷰 프레임의 후행 모서리를 나타내는 레이아웃 앵커
* _var_ widthAnchor: NSLayoutDimension 뷰 프레임의 너비를 나타내는 레이아웃 앵커

### 레이아웃 가이드와 같이 작업하기

* _func_ addLayoutGuide\(UILayoutGuide\) 지정된 레이아웃 가이드를 뷰에 추가합니다.
* _var_ layoutGuides: \[UILayoutGuide\] 이 뷰가 소유한 레이아웃 가이드 객체의 배열
* _var_ layoutMarginsGuide: UILayoutGuide 뷰 여백을 나타내는 레이아웃 가이드
* _var_ readableContentGuide: UILayoutGuide 뷰 내에서 읽을 수 있는 너비가 있는 영역을 나타내는 레이아웃 가이드
* _func_ removeLayoutGuide\(UILayoutGuide\) 지정된 레이아웃 가이드를 뷰에서 제거합니다.

### 자동 레이아웃에서 측정

* _func_ systemLayoutSizeFitting\(CGSize\) 현재 제약조건을 기준으로 뷰의 최적 크기를 반환합니다.
* _func_ systemLayoutSizeFitting\(CGSize, withHorizontalFittingPriority: UILayoutPriority, verticalFittingPriority: UILayoutPriority\) 제약조건과 지정된 맞춤 프로퍼티를 기준으로 하여 뷰의 최적 크기를 반환합니다.
* _var_ intrinsicContentSize: CGSize 뷰 자체의 프로퍼티만을 고려한 수신자 뷰의 자연 크기
* _func_ invalidateIntrinsicContentSize\(\) 뷰의 고유한 컨텐츠 사이즈를 무효화합니다.
* _func_ contentCompressionResistancePriority\(for: UILayoutConstraintAxis\) 뷰가 고유한 크기보다 작게 만들어지지 않도록 하는 우선순위를 반환합니다.
* _func_ setContentCompressionResistancePriority\(UILayoutPriority, for: UILayoutConstraintAxis\) 뷰가 고유한 크기보다 작게 만들어지지 않도록 하는 우선순위를 설정합니다.
* _func_ contentHuggingPriority\(for: UILayoutConstraintAxis\) 뷰가 고유한 크기보다 크게 만들어지지 않도록 하는 우선순위를 반환합니다.
* _func_ setContentHuggingPriority\(UILayoutPriority, for: UILayoutConstraintAxis\) 뷰가 고유한 크기보다 크게 만들어지지 않도록 하는 우선순위를 설정합니다.

### 자동 레이아웃에서 뷰 정렬

* _func_ alignmentRect\(forFrame: CGRect\) 지정된 프레임에 대한 뷰의 정렬 직사각형을 반환합니다.
* _func_ frame\(forAlignmentRect: CGRect\) 지정된 정렬 사각형에 대한 뷰 프레임을 반환합니다.
* _var_ alignmentRectInsets: UIEdgeInsets 정렬 직사각형을 정의하는 뷰 프레임의 inset
* ~~func forBaselineLayout\(\)~~ Returns a view used to satisfy baseline constraints. `Deprecated`
* _var_ forFirstBaselineLayout: UIView 첫 번째 기준선 제약조건을 충족하는 뷰를 반환합니다. Returns a view used to satisfy first baseline constraints.
* _var_ forLastBaselineLayout: UIView 마지막 기준선 제약조건을 충족하는 뷰를 반환합니다.

### 자동 레이아웃 시작시키기

* _func_ needsUpdateConstraints\(\) -&gt; Bool

  뷰가 제약조건을 업데이트 해야 할지 나타내는 Boolean 값을 반환합니다.

* _func_ setNeedsUpdateConstraints\(\)

  뷰의 제약조건 업데이트가 필요한지를 설정합니다.

* _func_ updateConstraints\(\)

  뷰 제약조건을 업데이트합니다.

* _func_ updateConstraintsIfNeeded\(\)

   수신자 뷰와 하위 뷰의 제약조건을 업데이트합니다.

### 자동 레이아웃 디버깅

제약조건 기반의 레이아웃 디버깅에 대한 자세한 내용은 [자동 레이아웃 가이드](https://melodyarchive.gitbook.io/sagwa/not-found)를 참조하세요.

* _func_ constraintsAffectingLayout\(for: UILayoutConstraintAxis\) 지정된 축에 대한 뷰 레이아웃에 영향을 미치는 제약조건을 반환합니다.
* _var_ hasAmbiguousLayout: Bool 뷰 레이아웃에 영향을 미치는 제약조건이 뷰의 위치를 불완전하게 지정하는지를 나타내는 Boolean 값
* _func_ exerciseAmbiguityInLayout\(\) 서로 다른 유효한 값으로 인해 발생하는 모호한 레이아웃을 통해 가능한 뷰 프레임을 랜덤하게 변화시켜 보입니다.

### 리사이징 동작 설정하기

경계가 변경될 때 컨텐츠를 조정하는 방법을 정의합니다.

* _var_ contentMode: UIViewContentMode 경계가 변경될 때 뷰가 내용의 표시방법을 결정하는데 사용되는 플래그입니다.
* _enum_ UIViewContentMode 경계가 변경될 때 뷰를 통해 컨텐츠를 조정하는 방법을 지정하는 옵션
* _func_ sizeThatFits\(CGSize\) 지정된 크기가장 적합한 크기를 계산하고 반환하도록 뷰에 요청합니다.
* _func_ sizeToFit\(\) 수신자 뷰의 크기를 조정하고 하위 뷰만 둘러싸도록 이동시킵니다.
* _var_ autoresizesSubviews: Bool 경계가 변경될 때 수신자 뷰가 자동적으로 하위 뷰의 크기를 재조정하게 할것인지를 결정하는 Boolean 값
* _var_ autoresizingMask: UIViewAutoresizing 상위 뷰의 경계가 변화할 때 수신자가 스스로 리사이징하는 방법을 결정하는 정수 비트마스크

### 하위 뷰 배치하기

앱이 자동 레이아웃을 사용하지 않는 경우 수동으로 뷰를 배치하세요.

* _func_ layoutSubviews\(\)

  하위 뷰를 배치합니다.

* _func_ setNeedsLayout\(\)

  수신자의 현재 레이아웃을 무효화시키고 다음 업데이트 사이클동안 레이아웃을 업데이트를 트리거합니다.

* _func_ layoutIfNeeded\(\)

  레이아웃 업데이트가 보류중인 경우 즉시 하위 뷰를 배치합니다.

* _class var_ requiresConstraintBasedLayout: Bool

  수신자가 제약조건 기반 레이아웃 시스템에 의존하고 있는지 나타내는 Boolean 값을 반환합니다.

* _var_ translatesAutoresizingMaskIntoConstraints: Bool

  뷰의 자동 크기지정 마스크가 자동 레이아웃 제약조건으로 변환되고 있는지를 나타내는 Boolean 값

### 유저 인터페이스 방향 관리

* _var_ semanticContentAttribute: UISemanticContentAttribute

  **왼쪽에서 오른쪽으로 쓰기**와 **오른쪽에서 왼쪽으로 쓰기**의 레이아웃 전환이 일어날때 뷰를 뒤집어야 할지 결정하는데 쓰이는 뷰 컨텐츠에 대한 시멘틱 설명

* _var_ effectiveUserInterfaceLayoutDirection: UIUserInterfaceLayoutDirection

  뷰의 컨텐츠를 즉각적으로 배치할때 적합한 유저 인터페이스 방향

* _class func_ userInterfaceLayoutDirection\(for: UISemanticContentAttribute\) -&gt; UIUserInterfaceLayoutDirection

  주어진 시멘틱 컨텐츠 속성에 대한 유저 인터페이스 방향을 반환합니다.

* _class func_ userInterfaceLayoutDirection\(for: UISemanticContentAttribute, relativeTo: UIUserInterfaceLayoutDirection\) -&gt; UIUserInterfaceLayoutDirection

  지정된 레이아웃 방향에 대해 시멘틱 컨텐츠 속성이 암시하는 레이아웃을 반환합니다.

### 드래그 앤 드롭 상호작용 지원

* _func_ addInteraction\(UIInteraction\)

  지정된 드래그 앤 드롭 또는 스프링로드 상호 작용을 뷰에 추가합니다.

* _func_ removeInteraction\(UIInteraction\) 지정된 드래그 앤 드롭 또는 스프링로드 상호 작용을 뷰에서 제거합니다.
* _var_ interactions: \[UIInteraction\]

  뷰의 상호작용의 배열

### 뷰의 그리기와 업데이트

* _func_ draw\(CGRect\)

  주어진 사각형 내에 수신자의 이미지를 그립니다.

* _func_ setNeedsDisplay\(\)

  수신자의 전체 경계 사각형이 다시 그려져야 함을 표시합니다.

* _func_ setNeedsDisplay\(CGRect\)

  수신자의 지정된 사각형이 다시 그려져야 함을 표시합니다.

* _var_ contentScaleFactor: CGFloat

  뷰에 적용된 축척 비율

* _func_ tintColorDidChange\(\)

  tintColor 프로퍼티가 변경될때 시스템에 의해 호출됩니다.

### 뷰 컨텐츠의 프린팅 서식지정

* _func_ viewPrintFormatter\(\) -&gt; UIViewPrintFormatter

  수신자 뷰의 print fommatter를 반환합니다.

* _func_ draw\(CGRect, for: UIViewPrintFormatter\)

  인쇄용 뷰의 컨텐츠를 그리기 위해 구현됩니다.

### 제스처 인식기 관리

* _func_ addGestureRecognizer\(UIGestureRecognizer\)

  뷰에 제스처 인식기를 연결합니다.

* _func_ removeGestureRecognizer\(UIGestureRecognizer\)

  뷰로부터 제스처 인식기를 제거합니다.

* _var_ gestureRecognizers: \[UIGestureRecognizer\]?

  현재 뷰에 연결되어있는 제스처 인식기 객체들

* _func_ gestureRecognizerShouldBegin\(UIGestureRecognizer\) -&gt; Bool

  제스처 인식기가 계속해서 터치 이벤트를 추적하도록 허용할 것인지를 묻습니다.

### 포커스 관찰하기

* _var_ canBecomeFocused: Bool

  뷰가 현재 포커스를 받을 수있는지 나타내는 Boolean 값

* _class var_ inheritedAnimationDuration: TimeInterval

  상속받은 현재 애니메이션의 지속시간을 반환한다.

* _var_ isFocused: Bool

  현재 해당 항목에 포커스가 주어졌는지를 나타내는 Boolean 값

### 모션효과 사용하기

* _func_ addMotionEffect\(UIMotionEffect\)

  뷰에 모션효과를 적용하기 시작합니다.

* _var_ motionEffects: \[UIMotionEffect\]

  뷰의 모션 효과 배열

* _func_ removeMotionEffect\(UIMotionEffect\)

  뷰에 모션효과를 적용하는 것을 중단합니다.

### 상태의 보존과 복구

* _var_ restorationIdentifier: String?

  뷰의 상태복원 지원 여부를 결정하는 식별자

* _func_ encodeRestorableState\(with: NSCoder\) 뷰에 대한 상태 관련 정보를 인코딩합니다.
* _func_ decodeRestorableState\(with: NSCoder\)

  뷰에 대한 상태관련 정보를 디코딩하고 복원합니다.

### 뷰 스냅샷 캡처하기

* _func_ snapshotView\(afterScreenUpdates: Bool\) -&gt; UIView?

  현재 뷰의 내용을 기반으로 스냅샷 뷰를 반환합니다.

* _func_ resizableSnapshotView\(from: CGRect, afterScreenUpdates: Bool, withCapInsets: UIEdgeInsets\) -&gt; UIView?

  현재 뷰의 지정된 내용을 기반으로 스냅샷 보기를 늘릴 수 있는 inset과 함께 반환합니다.

* _func_ drawHierarchy\(in: CGRect, afterScreenUpdates: Bool\) -&gt; Bool

  화면 상에 보이는 전체 뷰 계층 구조의 스냅샷을 현재 컨텍스트로 렌더링합니다.

### 런타임시 뷰 식별하기

* _var_ tag: Int

  앱에서 뷰 객체를 식별하는 데 사용할 수 있는 정수

* _func_ viewWithTag\(Int\) -&gt; UIView?

  지정된 값과 일치하는 태그를 가지고 있는 뷰를 반환합니다.

### 뷰 좌표계 간 변환

* _func_ convert\(CGPoint, to: UIView?\) -&gt; CGPoint

  수신자 좌표계의 포인트를 주어진 뷰의 좌표계로 변환합니다.

* _func_ convert\(CGPoint, from: UIView?\) -&gt; CGPoint 주어진 뷰 좌표계로부터의 포인트를, 수신자의 좌표계로 변환합니다.
* _func_ convert\(CGRect, to: UIView?\) -&gt; CGRect

  수신자 좌표계의 사각형을 주어진 뷰의 좌표계로 변환합니다.

* _func_ convert\(CGRect, from: UIView?\) -&gt; CGRect

  다른 뷰 좌표계의 사각형을 수신자의 좌표계로 변환합니다.

### 뷰에서 히트 테스팅

* _func_ hitTest\(CGPoint, with: UIEvent?\) -&gt; UIView?

  지정된 포인트를 포함하는 뷰 계층 구조\(수신자 포함\) 가장 먼 자손 객체를 반환합니다.

* _func_ point\(inside: CGPoint, with: UIEvent?\) -&gt; Bool

  수신자가 지정된 포인트를 포함하는지 나타내는 Boolean 값을 반환합니다.

### 뷰 에디팅 세션 종료하기

* _func_ endEditing\(Bool\) -&gt; Bool

  뷰 \(또는 포함된 텍스트 필드 중 하나\)가 첫번째 응답자 상태를 종료하도록 합니다.

### 접근성 동작 수정하기

* _var_ accessibilityIgnoresInvertColors: Bool

  뷰가 색상 반전을 위한 접근성 요청을 무시하는지 나타내는 Boolean 값

### 블럭으로 뷰 애니메이션시키기

다음 메서드들의 사용은 권장되지 않습니다. 대신 UIViewPropertyAnimator 클래스를 사용하세요.

* _class func_ animate\(withDuration: TimeInterval, delay: TimeInterval, options: UIView.AnimationOptions = \[\], animations: \(\) -&gt; Void, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  지정된 지속시간, 딜레이, 옵션 및 완료 핸들러를 사용해서 하나 이상의 뷰에 대한 변경사항을 애니메이션화합니다.

* _class func_ animate\(withDuration: TimeInterval, animations: \(\) -&gt; Void, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  지정된 지속시간과 완료 핸들러를 사용해서 하나 이상의 뷰에 대한 변경사항을 애니메이션화합니다.

* _class func_ animate\(withDuration: TimeInterval, animations: \(\) -&gt; Void\)

  지정된 지속시간동안 하나 이상의 뷰에 대한 변경사항을 애니메이션화합니다.

* _class func_ transition\(with: UIView, duration: TimeInterval, options: UIView.AnimationOptions = \[\], animations: \(\(\) -&gt; Void\)?, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  지정된 컨테이너 뷰에 대한 전환 애니메이션을 만듭니다.

* _class func_ transition\(from: UIView, to: UIView, duration: TimeInterval, options: UIView.AnimationOptions = \[\], completion: \(\(Bool\) -&gt; Void\)? = nil\)

  지정된 파라미터를 사용해, 지정된 뷰 간의 전환 애니메이션을 생성합니다.

* _class func_ animateKeyframes\(withDuration: TimeInterval, delay: TimeInterval, options: UIView.KeyframeAnimationOptions = \[\], animations: \(\) -&gt; Void, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  현재 뷰에서 키 프레임 기반 애니메이션을 설정하는 데 사용할 수 있는 애니메이션 블록 객체를 만듭니다.

* _class func_ addKeyframe\(withRelativeStartTime: Double, relativeDuration: Double, animations: \(\) -&gt; Void\)

  키 프레임 애니메이션의 단일 프레임에 대한 타이밍 및 애니메이션 값을 지정합니다.

* _class func_ perform\(UIView.SystemAnimation, on: \[UIView\], options: UIView.AnimationOptions = \[\], animations: \(\(\) -&gt; Void\)?, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  개발자가 정의한 선택적 병렬 애니메이션과 함께 하나 이상의 뷰에서 지정된 시스템 애니메이션을 수행합니다.

* _class func_ animate\(withDuration: TimeInterval, delay: TimeInterval, usingSpringWithDamping: CGFloat, initialSpringVelocity: CGFloat, options: UIView.AnimationOptions = \[\], animations: \(\) -&gt; Void, completion: \(\(Bool\) -&gt; Void\)? = nil\)

  스프링의 물리적 움직임에 대응하는 시간 커브를 사용하여 뷰 애니메이션을 실행합니다.

* _class func_ performWithoutAnimation\(\(\) -&gt; Void\)

  뷰 전환 애니메이션을 비활성화합니다.

### 뷰 애니메이션시키기

다음 메서드들의 사용은 권장지 않습니다. 대신 UIViewPropertyAnimator 클래스를 사용하여 애니메이션을 수행하세요.

* _class func_ beginAnimations\(String?, context: UnsafeMutableRawPointer?\)

  begin / commit 애니메이션 블록의 시작을 표시합니다.

* _class func_ commitAnimations\(\) begine / commit 애니메이션 블록의 끝을 표시하고 실행을 위해 애니메이션을 예약합니다.
* _class func_ setAnimationStart\(Date\)

  현재 애니메이션 블록의 시작 시간을 설정합니다.

* _class func_ setAnimationsEnabled\(Bool\)

  애니메이션의 사용 가능 여부를 설정합니다.

* _class func_ setAnimationDelegate\(Any?\)

  모든 애니메이션 메시지에 대한 delegate를 설정합니다.

* _class func_ setAnimationWillStart\(Selector?\)

  애니메이션이 시작될 때 애니메이션 delegate에게 보낼 메시지를 설정합니다.

* _class func_ setAnimationDidStop\(Selector?\)

  애니메이션이 중단 될 때 애니메이션 delegate에게 보낼 메시지를 설정합니다.

* _class func_ setAnimationDuration\(TimeInterval\)

  애니메이션 블록의 애니메이션 길이 \(초 단위\)를 설정합니다.

* _class func_ setAnimationDelay\(TimeInterval\) 애니메이션 블록 내에서 프로퍼티 변경 사항을 애니메이션화 하기 전에 대기 할 시간 \(초 단위\)을 설정합니다.
* _class func_ setAnimationCurve\(UIView.AnimationCurve\)

  애니메이션 블록 내에서 프로퍼티 변경 사항을 애니메이션화 할 때 사용할 곡선을 설정합니다.

* _class func_ setAnimationRepeatCount\(Float\)

  애니메이션 블록 내의 애니메이션이 반복되는 횟수를 설정합니다.

* _class func_ setAnimationRepeatAutoreverses\(Bool\)

  애니메이션 블록 내의 애니메이션을 자동으로 되돌릴지 설정합니다.

* _class func_ setAnimationBeginsFromCurrentState\(Bool\)

  현재 상태에서 애니메이션 재생을 시작할지 설정합니다.

* _class func_ setAnimationTransition\(UIView.AnimationTransition, for: UIView, cache: Bool\)

  애니메이션 블록에서 뷰에 적용할 전환을 설정합니다.

* _class var_ areAnimationsEnabled: Bool

  애니메이션이 활성화되었는지를 나타내는 부울 값을 반환합니다.

### 상수Constants

* _struct_ UIView.AnimationOptions

  블록 객체를 사용한 뷰 애니메이션에 적용되는 옵션

* _enum_ UIView.AnimationCurve

  지원되는 애니메이션 커브 지정

* _enum_ UIView.AnimationTransition 애니메이션 블록 객체에 사용하기 위한 애니메이션 전환 옵션
* _enum_ UIView.SystemAnimation

  애니메이션이 완료되면 계층에서 뷰를 제거하기 위한 옵션

* _struct_ UIView.KeyframeAnimationOptions

  animateKeyframes\(withDuration:delay:options:animations:completion:\) 메서드와 함께 사용되는 키 프레임 애니메이션 옵션.

* _enum_ NSLayoutConstraint.Axis

  객체 간 수평 또는 수직 레이아웃 제약조건을 지정하는 키

* _enum_ UIView.TintAdjustmentMode

  뷰의 tint 조정모드

* _class let_ layoutFittingCompressedSize: CGSize

  가능한 가장 작은 크기를 사용하는 옵션

* _class let_ layoutFittingExpandedSize: CGSize 가능한 가장 큰 크기를 사용하는 옵션
* _class let_ noIntrinsicMetric: CGFloat

  주어진 숫자 뷰 프로퍼티에 고유한 메트릭이 존재하지 않음

* _struct_ UIView.AutoresizingMask

  자동 뷰 리사이징 옵션

* _enum_ UISemanticContentAttribute

  **왼쪽에서 오른쪽으로 쓰기**와 **오른쪽에서 왼쪽으로 쓰기**의 레이아웃 전환이 일어날때 뷰를 뒤집어야 할지 결정하는데 쓰이는 뷰 컨텐츠에 대한 시멘틱 설명

## 관련 문서

### 상속받은 대상

* [UIResponder](https://melodyarchive.gitbook.io/sagwa/uikit/touches_presses_and_gestures/uiresponder)

### 준수하는 프로토콜

* CALayerDelegate
* CVarArg
* Equatable
* Hashable
* NSCoding
* UIAccessibilityIdentification
* UIAppearance
* UIAppearanceContainer
* UICoordinateSpace
* UIDynamicItem
* UIFocusItem
* UIPasteConfigurationSupporting
* UITraitEnvironment

