# playback

> 원본 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616509-playback](https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616509-playback)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
static let playback: AVAudioSession.Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
const AVAudioSessionCategory AVAudioSessionCategoryPlayback;
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

이 category를 사용한 앱의 오디오는 스크린이 잠겼을 때나 무음 스위치가 켜졌을 때에도 계속됩니다. 앱이 백그라운드로 전환 \(예를 들어, 화면이 잠길 때\)된 후에도 오디오를 계속해서 재생하기 위해서는 정보 속성 리스트\(plist\)의 [UIBackgroundModes](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/iPhoneOSKeys.html#//apple_ref/doc/plist/info/UIBackgroundModes) 키에 `audio` 값을 추가하세요.

기본적으로 이 category를 사용한다는 것은 앱의 오디오가 믹스될 수 없음을 의미하며 해당 category의 오디오 세션을 활성화 시킬 경우 믹스될 수 없는 다른 오디오 세션을 중단시킬 것입니다. 이 category가 믹스될 수 있게 하려면 [`mixWithOthers`](https://developer.apple.com/documentation/avfoundation/avaudiosession/categoryoptions/1616611-mixwithothers) 옵션을 사용하세요.

