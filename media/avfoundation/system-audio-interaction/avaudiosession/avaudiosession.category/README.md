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
> * macOS 10.15+
> * Mac Catalyst 13.0+
> * tvOS 12.0+
> * watchOS 5.0+
>
> **Framework**
>
> * AVFoundation

## 개요

오디오 세션 카테고리는 오디오 동작 집합을 정의합니다. 운영체제는 각 카테고리별로 정확한 동작을 설정하고 애플은 운영체제 버전을 업그레이드하면서 카테고리의 동작을 개선할 수도 있습니다.

[AVAudioSession.Mode](../avaudiosession.mode.md)에 설명대로 오디오 세션 모드를 사용하여 [playback](playback.md), [record](record.md), [playAndRecord](playandrecord.md) 카테고리가 제공하는 설정들을 세부 조정할 수 있습니다.



### 에어플레이 지원

재생만 지원하는 오디오 세션 카테고리\([ambient](ambient.md), [soloAmbient](soloambient.md), [playback](playback.md)\)는 \(비\)미러링 에어플레이를 지원합니다.

[playAndRecord](playandrecord.md) 카테고리는 미러링 방식의 에어플레이만 지원하며 [record](record.md)와 [multiRoute](untitled.md) 카테고리는 에어플레이를 지원하지 않습니다.

## 주제

### 오디오 세션 카테고리

* _static_ _let_ [ambient](ambient.md): AVAudioSessioin.Category 소리 재생이 주요기능이 아닌 앱을 위한 Category. 즉, 이 Category가 적용된 앱은 소리가 꺼진 상태에서도 성공적으로 동작합니다.
* _static_ _let_ [multiRoute](untitled.md): AVAudioSessioin.Category 개별 오디오 데이터 스트림을 서로 다른 출력 장치로 동시에 라우팅 시키기 위한 Category.
* _static_ _let_ [playAndRecord](playandrecord.md): AVAudioSessioin.Category 오디오 녹음\(입력\)및 재생\(출력\)을 위한 Category. VoIP \(Voice over Internet Protocol\) 앱 같은 곳에 쓰입니다.
* _static_ l_e_t [playback](playback.md): AVAudioSessioin.Category 사용하는데 있어서 녹음된 음악이나 소리 재생이 중요한 앱에 사용되는 Category.
* _static_ _let_ [record](record.md): AVAudioSession.Category 오디오 녹음을 위한 Category. 이 Category는 playback 오디오를 음소거시킵니다.
* _static_ _let_ [soloAmbient](soloambient.md): AVAudioSessioin.Category 기본 audio session category.
* ~~_static_ _let_ audioProcessing: AVAudioSessioin.Category The category for using an audio hardware codec or signal processor while not playing or recording audio.~~ `Deprecated`

### Initializers

* init\(rawValue: String\)



## 관련 문서

### 준수하는 프로토콜

* Equatable
* Hashable
* RawRepresentable

## 같이 보기

### 오디오 세션 설정 <a id="configuring-the-audio-session"></a>

* _var_ category: AVAudioSession.Category 현재 오디오 세션 카테고리
* _func_ setCategory\(AVAudioSession.Category\) 현재 오디오 세션 카테고리를 새로 설정합니다.
* _var_ availableCategories: \[AVAudioSession.Category\] 현재 기기에서 사용가능한 오디오 세션 카테고리
* _var_ categoryOptions: AVAudioSession.CategoryOptions 현재 오디오 세션 카테고리와 관련된 옵션 마스크
* _func_ setCategory\(AVAudioSession.Category, options: AVAudioSession.CategoryOptions\) 오디오 세션 카테고리를 지정된 옵션과 같이 설정합니다.
* struct AVAudioSession.CategoryOptions 오디오 동작 옵션을 가리키는 상수
* _var_ mode: AVAudioSession.Mode 현재 오디오 세션 모드
* _func_ setMode\(AVAudioSession.Mode\)

  현재 오디오 세션 모드를 설정합니다.

* _func_ setCategory\(AVAudioSession.Category, mode: AVAudioSession.Mode, options: AVAudioSession.CategoryOptions\) 오디오 세션을 지정된 카테고리, 모드, 옵션으로 설정합니다.
* _var_ availableModes: \[AVAudioSession.Mode\] 현재 기기에서 사용가능한 오디오 세션 모드
* _struct_ [AVAudioSession.Mode](../avaudiosession.mode.md) 오디오 세션 모드 식별자
* _var_ routeSharingPolicy: AVAudioSession.RouteSharingPolicy 현재 라우트 공유 정책
* _func_ setCategory\(AVAudioSession.Category, mode: AVAudioSession.Mode, policy: AVAudioSession.RouteSharingPolicy, options: AVAudioSession.CategoryOptions\) 오디오 세션을 지정된 카테고리, 모드, 라우트 공유 정책, 옵션으로 설정합니다.
* _enum_ AVAudioSession.RouteSharingPolicy 오디오 세션에 사용 가능한 라우트 공유 정책을 가리킵니다.

