---
description: 지정된 뷰의 좌표계 내에서의 제스처 이동
---

# translation\(in:\)

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uipangesturerecognizer/1621207-translation](https://developer.apple.com/documentation/uikit/uipangesturerecognizer/1621207-translation)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
func translation(in view: UIView?) -> CGPoint
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
- (CGPoint)translationInView:(UIView *)view;
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

* view 좌표계 내의 팬 제스처 이동을 계산해내는 뷰입니다. 뷰를 계속해서 사용자 손가락 밑에 위치시키고 싶다면 수퍼뷰 좌표계에서의 좌표를 요청하세요.

## Return Value

지정된 수퍼뷰의 좌표계에서 뷰의 새 위치를 가리키는 점.

## Discussion

x/y 값은 시간에 따른 전체적인 이동을 보고합니다. 이것은 직전에 보고된 translation과의 델타값이 아닙니다. 제스처가 처음 인식될 때 translation값을 뷰의 상태값으로 적용시키되 핸들러가 호출될 때마다 값을 합산하지 마세요.

## 같이 보기

### 제스처 위치와 속도 추적

* _func_ [setTranslation\(CGPoint, in: UIView?\)](settranslation-_-in.md) 지정된 뷰의 좌표계 내에서의 좌표를 설정합니다.
* _func_ [velocity\(in: UIView?\)](velocity-in.md) -&gt; CGPoint 지정된 뷰의 좌표계 내에서의 제스처 속도

