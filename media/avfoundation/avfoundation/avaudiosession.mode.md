# AVAudioSession.Mode

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
struct Mode
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
typedef NSString *AVAudioSessionMode;
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

* _static_ _let_ default: AVAudioSession.Mode 기본 오디오 세션 모드
* _static_ _let_ gameChat: AVAudioSession.Mode 이 모드는 Game Kit의 Voice chat 서비스를 사용하는 애플리케이션에서 Game Kit이 대신해서 설정하는 모드입니다.
* _static_ _let_ measurement: AVAudioSession.Mode 앱이 오디오의 입출력을 측정할 때 사용하세요.
* _static_ _let_ moviePlayback: AVAudioSession.Mode 앱이 영상 컨텐츠를 재생하는 경우에 사용하세요.
* _static_ _let_ spokenAudio: AVAudioSession.Mode 본인의 앱에서 연속적인 음성 오디오를 재생하고 있고, 다른 앱에서 짧은 길이의 음성 오디오가 재생될때 오디오를 일시 정지시키고 싶은 경우에 사용하는 모드.
* _static_ _let_ videoChat: AVAudioSession.Mode 온라인 비디오 회의에 참여할 때 사용하는 모드.
* _static_ _let_ videoRecording: AVAudioSession.Mode 앱이 비디오를 녹음할 때 사용하는 모드.
* _static_ _let_ voiceChat: AVAudioSession.Mode VoIP와 같은 양방향 음성 커뮤니케이션을 수행할 때 사용하는 모드.
* _static_ _let_ voicePrompt: AVAudioSession.Mode

