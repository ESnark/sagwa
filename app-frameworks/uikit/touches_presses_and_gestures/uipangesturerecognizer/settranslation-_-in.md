---
description: 지정된 뷰의 좌표계 내에서의 좌표를 설정합니다.
---

# setTranslation\(\_:in:\)

> 원문 출처  
> [https://developer.apple.com/documentation/uikit/uipangesturerecognizer/1621206-settranslation](https://developer.apple.com/documentation/uikit/uipangesturerecognizer/1621206-settranslation)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
func setTranslation(_ translation: CGPoint,
                in view: UIView?)
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
- (void)setTranslation:(CGPoint)translation 
                inView:(UIView *)view;
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

* translation 새 이동값을 가리키는 점.
* view 이동이 일어나는 좌표계의 뷰.

## Discussion

이동값을 변경하면 팬의 속도가 리셋됩니다.

## 같이 보기

### 제스처 위치와 속도 추적

* _func_ [translation\(in: UIView?\)](translation-in.md) -&gt; CGPoint 지정된 뷰의 좌표계 내에서의 제스처 이동
* _func_ [velocity\(in: UIView?\)](velocity-in.md) -&gt; CGPoint 지정된 뷰의 좌표계 내에서의 제스처 속도

