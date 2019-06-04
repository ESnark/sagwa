---
description: 지정된 뷰의 좌표계 내에서의 제스처 속도
---

# velocity\(in:\)

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uipangesturerecognizer/1621209-velocity](https://developer.apple.com/documentation/uikit/uipangesturerecognizer/1621209-velocity)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
func velocity(in view: UIView?) -> CGPoint
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
- (CGPoint)velocityInView:(UIView *)view;
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

## Parameters

* view 좌표계 내의 팬 제스처 속도를 계산해내는 뷰.

## Return Value

초당 포인트로 계산되는 팬 제스처의 속도. 속도는 수평이동속도와 수직이동속도로 나뉩니다.

## 같이 보기

### 제스처 위치와 속도 추적

* _func_ [translation\(in: UIView?\)](translation-in.md) -&gt; CGPoint 지정된 뷰의 좌표계 내에서의 제스처 이동
* _func_ [setTranslation\(CGPoint, in: UIView?\)](settranslation-_-in.md) 지정된 뷰의 좌표계 내에서의 좌표를 설정합니다.

