# record

> 원본 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616451-record](https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616451-record)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
static let record: AVAudioSession.Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
const AVAudioSessionCategory AVAudioSessionCategoryRecord;
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

이 category는 세션이 활성화되는 동안 시스템상의 거의 모든 출력을 음소거시킵니다. 예상치 못하게 재생중인 소리를 막을 필요가 없다면 [`playAndRecord`](playandrecord.md)를 대신 사용하는 것을 추천합니다. 앱이 백그라운드로 전환 \(예를 들어, 화면이 잠길 때\)된 후에도 오디오를 계속해서 녹음하기 위해서는 정보 속성 리스트\(plist\)의 [UIBackgroundModes](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/iPhoneOSKeys.html#//apple_ref/doc/plist/info/UIBackgroundModes) 키에 `audio` 값을 추가하세요.

오디오 녹음을 위해서는 사용자의 권한 허가가 필요합니다. \(_사용자 권한이 필요한 녹음_을 읽어보세요.\)

{% hint style="info" %}
Note

이 category는 전화벨 소리나 알람, 다른 믹스될 수 없는 오디오 세션으로 인해서 해당 오디오 세션이 중단되는 것을 막을 수 없습니다.
{% endhint %}



