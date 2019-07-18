---
description: 동일한 view 내에서 여러 제스처 인식기를 사용하는 방법을 알아보세요.
---

# 다중 제스처 인식기 조정

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/touches\_presses\_and\_gestures/coordinating\_multiple\_gesture\_recognizers](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/coordinating_multiple_gesture_recognizers)

## 개요

각각의 제스처 인식기들은 들어오는 터치 이벤트를 별도로 추적합니다. 하지만 UIKit은 일반적으로 하나의 뷰에서 한번에 하나의 제스처만 인식하도록 하고 있습니다. 하나의 제스처만 인식하여 사용하면 입력이 하나 이상의 액션을 일으키는 것을 막아줄 수 있기 때문에 대부분의 경우에 선호되는 방식이지만 이 기본 동작이 의도치 않은 부작용을 일으키기도 합니다. 예를 들어 팬과 스와이프 제스처 인식기를 둘다 보유하고 있는 뷰가 하나 있다고 가정해봅시다. 팬 제스처 인식기는 연속적이고, 스와이프 제스처 인식기는 불연속적이기 때문에 스와이프 인식기는 절대로 사용될 수 없을것입니다.

이렇게 기본 인식 동작으로부터 발생하는 부작용을 막기 위해서는 delegate 객체를 사용하여 UIKit에 제스처의 인식 순서를 알려줘야 합니다. UIKit은 delegate 객체의 메서드를 사용해서 제스처 인식기 간의 순서를 결정합니다. 예를 들어 팬 제스처 인식기가 동작을 취하기 위해서는 그 전에 스와이프 제스처 인식기가 실패한 이후에만 가능하다든지, 두 제스처가 동식에 인식될 수 있다든지 하는 내용을 delegate를 통해서 UIKit에 전달할 수 있습니다.

## 주제

### 동시 제스처

* 하나의 제스처가 다른 제스처보다 우선하는 경우 제스처 인식기의 delegate 객체를 사용해서 뷰 안의 제스처 우선순위를 결정하세요
* 여러 제스처의 동시 인식 허용 delegate 객체를 사용해서 하나 이상의 제스처를 동시에 감지하는 방법을 알아보세요
* UIKit 컨트롤에 제스처 인식기 연결 제스처 인식기가 버튼이나 스위치 같은 UIKit 컨트롤과 어떻게 상호작용하는지 알아보세요

## 같이 보기

### 표준 제스처

* [UIKit 제스처 처리](handling_uikit_gestures.md) 제스처 인식기를 사용하여 터치 처리를 단순화하고 일관적인 사용자 환경을 만드세요.
* _class_ UIHoverGestureRecognizer `beta` A gesture recognizer that looks for pointer movement over a view.
* _class_ [UILongPressGestureRecognizer](uilongpressgesturerecognizer.md) 길게 누르기 제스처를 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스
* _class_ [UIPanGestureRecognizer](uipangesturerecognizer/) 드래그 제스처를 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스
* _class_ UIPinchGestureRecognizer pinching 제스처를 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스
* _class_ UIScreenEdgePanGestureRecognizer 스크린 가장자리로부터의 드래그 제스처를 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스
* _class_ UISwipeGestureRecognizer 하나 이상의 방향으로 스와이프하는 제스처를 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스
* _class_ UIRotationGestureRecognizer 두 개의 터치로 회전하는 제스처를 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스
* _class_ UITapGestureRecognizer 하나 또는 다중 탭 동작을 인식하는 [UIGestureRecognizer](uigesturerecognizer.md)의 하위 구상 클래스

