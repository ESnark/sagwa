---
description: 시스템 오디오를 앱에 통합시키세요.
---

# 시스템 오디오 상호작용

> 원문 출처  
> [https://developer.apple.com/documentation/avfoundation/system\_audio\_interaction](https://developer.apple.com/documentation/avfoundation/system_audio_interaction)

## 개요

시스템 오디오와 상호작용하려면 AVAudioSession 클래스를 사용해서 다음 작업들을 수행하세요

* 시스템과 통신하여 앱에서 오디오를 어떻게 사용할 것지를 알리세요.
* 앱의 AudioSession을 활성화시키세요.
* 오디오 녹음 권한을 요청하세요.
* 오디오 인터럽트나 라우트 변경 같은 이벤트를 알려주는 AudioSession 노티피케이션을 등록하고 응답하세요.
* Sample rate, I/O 버퍼 지속시간, 채널 갯수 등 오디오 디바이스에 대한 고급 설정을 수행하세요.

## 주제

### AudioSession 사용

* _class_ [AVAudioSession](avaudiosession.md) 앱에서 오디오를 사용하는 방식을 시스템에 전달하는 중간 객체

### 권한

* 앱 간 오디오 권한 부여 앱 간 오디오를 지원하는 다른 앱과 오디오를 교환하도록 할 것인지를 지정하는 Boolean 값

## 같이 보기

* 오디오 트랙 엔지니어링 오디오를 재생, 녹음, 믹스, 처리하세요.



