---
description: 오디오 세션 모드 식별자
---

# AVAudioSession.Mode

> 원문 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/mode](https://developer.apple.com/documentation/avfoundation/avaudiosession/mode)

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
> * macOS 10.15+
> * Mac Catalyst 13.0+
> * tvOS 12.0+
> * watchOS 5.0+

> **Framework**
>
> * AVFoundation

## 개요

카테고리는 앱의 기본 동작을 설정하고, 모드는 특화된 동작을 오디오 세션 카테고리에 적용합니다.

{% hint style="warning" %}
Important

오디오 세션 카테고리에 해당 카테고리가 지원하지 않는 모드를 지정하면 오디오 세션은 자동으로 default 모드를 사용하게 됩니다. \(예: multiRoute 카테고리에 gameChat 모드 적용\)
{% endhint %}

## 주제

### AudioSessioin Modes

* _static_ _let_ default: AVAudioSession.Mode 기본 오디오 세션 모드
* _static_ _let_ gameChat: AVAudioSession.Mode 이 모드는 Game Kit의 Voice chat 서비스를 사용하는 애플리케이션에서 Game Kit이 대신해서 설정하는 모드입니다.
* _static_ _let_ measurement: AVAudioSession.Mode 앱이 오디오의 입출력을 측정할 때 사용하세요.
* _static_ _let_ moviePlayback: AVAudioSession.Mode 앱이 영상 컨텐츠를 재생하는 경우에 사용하세요.
* _static_ _let_ spokenAudio: AVAudioSession.Mode 본인의 앱에서 연속적인 음성 오디오를 재생하고 있고, 다른 앱에서 짧은 길이의 음성 오디오가 재생될때 오디오를 일시 정지시키고 싶은 경우에 사용하는 모드.
* _static_ _let_ videoChat: AVAudioSession.Mode 온라인 비디오 회의에 참여할 때 사용하는 모드.
* _static_ _let_ videoRecording: AVAudioSession.Mode 앱이 비디오를 녹음할 때 사용하는 모드.
* _static_ _let_ voiceChat: AVAudioSession.Mode VoIP와 같은 양방향 음성 커뮤니케이션을 수행할 때 사용하는 모드.
* _static_ _let_ voicePrompt: AVAudioSession.Mode TTS 오디오를 재생하는 앱에서 사용하는 모드.

### Initializers

* init\(rawValue: String\)

## 관련 문서

### 준수하는 프로토콜

Equatable, Hashable, RawRepresentable

## 같이 보기

### 오디오 세션 설정 <a id="configuring-the-audio-session"></a>

* _var_ category: AVAudioSession.Category 현재 오디오 세션 카테고리
* _func_ setCategory\(AVAudioSession.Category\) 현재 오디오 세션 카테고리를 새로 설정합니다.
* _var_ availableCategories: \[AVAudioSession.Category\] 현재 기기에서 사용가능한 오디오 세션 카테고리
* _struct_ [AVAudioSession.Category](avaudiosession.category/) 오디오 세션 카테고리 식별자
* _var_ categoryOptions: AVAudioSession.CategoryOptions 현재 오디오 세션 카테고리와 관련된 옵션 마스크
* _func_ setCategory\(AVAudioSession.Category, options: AVAudioSession.CategoryOptions\) 오디오 세션 카테고리를 지정된 옵션과 같이 설정합니다.
* struct AVAudioSession.CategoryOptions 오디오 동작 옵션을 가리키는 상수
* _var_ mode: AVAudioSession.Mode 현재 오디오 세션 모드
* _func_ setMode\(AVAudioSession.Mode\)

  현재 오디오 세션 모드를 설정합니다.

* _func_ setCategory\(AVAudioSession.Category, mode: AVAudioSession.Mode, options: AVAudioSession.CategoryOptions\) 오디오 세션을 지정된 카테고리, 모드, 옵션으로 설정합니다.
* _var_ availableModes: \[AVAudioSession.Mode\] 현재 기기에서 사용가능한 오디오 세션 모드
* _struct_ [AVAudioSession.Mode](avaudiosession.mode.md) 오디오 세션 모드 식별자
* _var_ routeSharingPolicy: AVAudioSession.RouteSharingPolicy 현재 라우트 공유 정책
* _func_ setCategory\(AVAudioSession.Category, mode: AVAudioSession.Mode, policy: AVAudioSession.RouteSharingPolicy, options: AVAudioSession.CategoryOptions\) 오디오 세션을 지정된 카테고리, 모드, 라우트 공유 정책, 옵션으로 설정합니다.
* _enum_ AVAudioSession.RouteSharingPolicy 오디오 세션에 사용 가능한 라우트 공유 정책을 가리킵니다.

\_\_

