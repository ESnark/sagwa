---
description: 길게 누르기 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
---

# UILongPressGestureRecognizer

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uilongpressgesturerecognizer](https://developer.apple.com/documentation/uikit/uilongpressgesturerecognizer)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class UILongPressGestureRecognizer: UIGestureRecognizer
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface UILongPressGestureRecognizer : UIGestureRecognizer
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

이 동작을 트리거시키려면 사용자가 하나 이상의 손가락으로 뷰를 일정 시간동안 누르고 있어야 합니다. 누르고 있는 동안 손가락이 일정 거리 이상을 움직이게 된다면 해당 제스처는 실패하게 됩니다.

롱 프레스 제스처는 연속적입니다. 이 제스처는 허용된 수 만큼의 손가락이 \(numberOfTouchesRequired\) 일정 시간동안 \(minimumPressDuration\) 터치가 허락된 거리 범위\(allowableMovement\) 이상으로 움직이지 않을 때 시작됩니다. \(UIGestureRecognizer.State.began\) 제스처 인식기는 손가락이 움직일 때마다 변경 상태로 전환되고 손가락이 들렸을 때 끝납니다. \(UIGestureRecognizer.State.ended\)

## 주제

### 제스처 인식기 설정

* _var_ minimumPressDuration: TimeInterval 제스처가 인식되기 위해서 누르고 있어야 하는 최소 시간.
* _var_ numberOfTouchesRequired: Int 제스처가 인식되기 위해서 눌러야 하는 손가락의 갯수
* _var_ numberOfTapsRequired: Int 제스처가 인식되기 위해서 필요한 탭 수
* _var_ allowableMovement: CGFloat 제스처가 실패하지 않는 손가락의 최대 이동거리



## 관련 문서

### 상속받은 대상

* UIGestureRecognizer

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

## 같이 보기

### 표준 제스처

* [UIKit 제스처 처리](handling_uikit_gestures.md) 제스처 인식기를 사용하여 터치 처리를 단순화하고 일관적인 사용자 환경을 만드세요.
* 다중 제스처 인식기 조정 동일한 view 내에서 여러 제스처 인식기를 사용하는 방법을 알아보세요.
* _class_ UIHoverGestureRecognizer `beta` A gesture recognizer that looks for pointer movement over a view.
* _class_ [UIPanGestureRecognizer](uipangesturerecognizer/) 드래그 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UIPinchGestureRecognizer pinching 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UIScreenEdgePanGestureRecognizer 스크린 가장자리로부터의 드래그 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UISwipeGestureRecognizer 하나 이상의 방향으로 스와이프하는 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UIRotationGestureRecognizer 두 개의 터치로 회전하는 제스처를 인식하는 UIGestureRecognizer의 하위 구상 클래스
* _class_ UITapGestureRecognizer 하나 또는 다중 탭 동작을 인식하는 UIGestureRecognizer의 하위 구상 클래스

