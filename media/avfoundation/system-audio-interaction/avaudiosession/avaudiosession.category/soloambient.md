# soloAmbient

> 원문 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616488-soloambient](https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616488-soloambient)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
static let soloAmbient: AVAudioSession.Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
const AVAudioSessionCategory AVAudioSessionCategorySoloAmbient;
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

이 category를 사용하는 경우 스크린이 잠기거나 무음 스위치가 켜졌을 때 음소거됩니다.

기본적으로 이 category를 사용한다는 것은 앱의 오디오가 믹스될 수 없음을 의미하며 해당 category의 오디오 세션을 활성화 시킬 경우 믹스될 수 없는 다른 오디오 세션을 중단시킬 것입니다. 믹스를 허용하고자 한다면 [`ambient`](ambient.md) category를 대신 사용하세요.

