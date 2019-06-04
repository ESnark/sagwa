---
description: 드래그 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
---

# UIPanGestureRecognizer

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uipangesturerecognizer](https://developer.apple.com/documentation/uikit/uipangesturerecognizer)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class UIPanGestureRecognizer: UIGestureRecognizer
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface UIPanGestureRecognizer : UIGestureRecognizer
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

## 개요

사용자는 팬\(드래그\)하는 동안 하나 이상의 손가락으로 뷰를 누르고 있어야 합니다. 이 동작 메서드를 구현하는 클라이언트는 제스처 인식기에게 현재 이동 및 속도에 대한 값을 요청할 수 있습니다.

패닝 제스처는 연속적입니다. 이 제스처는 필요한 최소 갯수의 손가락이 \([minimumNumberOfTouches](minimunnumberoftouches.md)\) 팬으로 인식될 만큼의 거리를 이동했을 때 시작됩니다. \(UIGestureRecognizer.State.began\) 최소 요구되는 손가락이 터치된 상태로 움직일 때 변경되고, \(UIGestureRecognizer.State.changed\) 모든 손가락이 들어올려지면 끝납니다. \(UIGestureRecognizer.State.ended\)

이 클래스의 클라이언트는 동작 메서드를 통해서 UIPanGestureRecognizer 객체에 현재 제스처의 좌표와 \([translation\(in:\)](translation-in.md)\) 속도를 \([velocity\(in:\)](velocity-in.md)\) 요청할 수 있습니다. 이 메서드들에 주어지는 뷰를 기준 좌표계로 하여 이동/속도값을 얻어낼 수 있습니다. 또한 클라이언트는 원하는 값으로 좌표를 리셋할 수 있습니다.

## 주제

### 제스처 인식기 설정

* _var_ [maximumNumberOfTouches](maximumnumberoftouches.md): Int 제스처로 인식 가능한 터치 손가락의 최대 숫자
* _var_ [minimunNumberOfTouches](minimunnumberoftouches.md): Int 제스처로 인식 가능한 터치 손가락의 최소 숫자

### 제스처 위치와 속도 추적

* _func_ [translation\(in: UIView?\)](translation-in.md) -&gt; CGPoint 지정된 뷰의 좌표계 내에서의 제스처 이동
* _func_ [setTranslation\(CGPoint, in: UIView?\)](settranslation-_-in.md) 지정된 뷰의 좌표계 내에서의 좌표를 설정합니다.
* _func_ [velocity\(in: UIView?\)](velocity-in.md) -&gt; CGPoint 지정된 뷰의 좌표계 내에서의 제스처 속도

## 관련 문서

### 상속받은 대상

* UIGestureRecognizer

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

### 표준 제스처

* [UIKit 제스처 처리](../handling_uikit_gestures.md) 제스처 인식기를 사용하여 터치 처리를 단순화하고 일관적인 사용자 환경을 만드세요.
* 다중 제스처 인식기 조정 동일한 view 내에서 여러 제스처 인식기를 사용하는 방법을 알아보세요.
* _class_ UIHoverGestureRecognizer `beta` A gesture recognizer that looks for pointer movement over a view.
* _class_ [UILongPressGestureRecognizer](../uilongpressgesturerecognizer.md) 길게 누르기 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UIPinchGestureRecognizer pinching 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UIScreenEdgePanGestureRecognizer 스크린 가장자리로부터의 드래그 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UISwipeGestureRecognizer 하나 이상의 방향으로 스와이프하는 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UIRotationGestureRecognizer 두 개의 터치로 회전하는 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UITapGestureRecognizer 하나 또는 다중 탭 동작을 인식하는 UIGestureRecognizer의 하위 구상 클래스

