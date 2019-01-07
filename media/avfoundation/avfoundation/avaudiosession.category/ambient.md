# ambient

> 원본 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616560-ambient](https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616560-ambient)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
static let ambient: AVAudioSession.Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
const AVAudioSessionCategory AVAudioSessionCategoryAmbient;
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 3.0+
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * AVFoundation

## Discussion

이 Category는 음악 앱이 재생중일때 사용자가 연주하는 가상 피아노와 같이 "같이 재생하는" 스타일의 앱에 적합합니다. 이 Category를 사용할 때에는 다른 앱에서 나오는 오디오가 여러분의 오디오와 섞입니다. 또한 이 Category가 적용되고 있을 때는 화면잠금이나 \(아이폰에서는 벨소리/무음 스위치로 동작하는\) 무음 모드일때 오디오가 꺼집니다.

