# AVAudioSession.Category

> 원문 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category](https://developer.apple.com/documentation/avfoundation/avaudiosession/category)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
struct Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
typedef NSString *AVAudioSessionCategory;
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 12.0+
> * tvOS 12.0+
> * watchOS 5.0+
>
> **Framework**
>
> * AVFoundation

## 주제

### Initializers

* init\(rawValue: String\)

### Type Properties

* _static_ _let_ [ambient](ambient.md): AVAudioSessioin.Category 소리 재생이 주요기능이 아닌 앱을 위한 Category. 즉, 이 Category가 적용된 앱은 소리가 꺼진 상태에서도 성공적으로 동작합니다.
* ~~_static_ _let_ audioProcessing: AVAudioSessioin.Category The category for using an audio hardware codec or signal processor while not playing or recording audio.~~ `Deprecated`
* _static_ _let_ [multiRoute](untitled.md): AVAudioSessioin.Category 개별 오디오 데이터 스트림을 서로 다른 출력 장치로 동시에 라우팅 시키기 위한 Category.
* _static_ _let_ [playAndRecord](playandrecord.md): AVAudioSessioin.Category 오디오 녹음\(입력\)및 재생\(출력\)을 위한 Category. VoIP \(Voice over Internet Protocol\) 앱 같은 곳에 쓰입니다.
* _static_ l_e_t playback: AVAudioSessioin.Category 사용하는데 있어서 녹음된 음악이나 소리 재생이 중요한 앱에 사용되는 Category.
* _static_ _let_ record: AVAudioSession.Category 오디오 녹음을 위한 Category. 이 Category는 playback 오디오를 음소거시킵니다.
* _static_ _let_ soloAmbient: AVAudioSessioin.Category 기본 audio session category.



