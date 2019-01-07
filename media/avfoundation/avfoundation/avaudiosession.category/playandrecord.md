# playAndRecord

> 원본 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616568-playandrecord](https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616568-playandrecord)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
static let playAndRecord: AVAudioSession.Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
const AVAudioSessionCategory AVAudioSessionCategoryPlayAndRecord;
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

오디오는 아이폰의 무음 스위치가 켜져있거나 스크린이 잠겨 있더라도 계속해서 재생될 수 있습니다. 앱이 백그라운드로 전환 \(예를 들어, 화면이 잠길 때\)된 후에도 오디오를 계속해서 재생하기 위해서는 정보 속성 리스트\(plist\)의 [UIBackgroundModes](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/iPhoneOSKeys.html#//apple_ref/doc/plist/info/UIBackgroundModes) 키에 `audio` 값을 추가하세요.

이 category는 녹음과 재생을 동시에 하거나, \(동시에 하지 않더라도\) 둘 다 하는 앱에 적합합니다.

기본적으로 이 category를 사용한다는 것은 앱의 오디오가 믹스될 수 없음을 의미하며 해당 category의 오디오 세션을 활성화 시킬 경우 믹스될 수 없는 다른 오디오 세션을 중단시킬 것입니다. 이 category가 믹스될 수 있게 하려면 [`mixWithOthers`](https://developer.apple.com/documentation/avfoundation/avaudiosession/categoryoptions/1616611-mixwithothers) 옵션을 사용하세요.

오디오 녹음을 위해서는 사용자의 권한 허가가 필요합니다. \(_사용자 권한이 필요한 녹음_을 읽어보세요.\)

이 category는 미러링된 에어플레이를 지원합니다. 그러나 `AVAudioSessionModeVoiceChat` 모드를 사용하게 되면 AirPlay 미러링은 비활성화됩니다.

