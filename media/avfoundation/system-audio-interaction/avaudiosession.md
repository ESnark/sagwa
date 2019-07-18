---
description: 앱에서 오디오를 사용하는 방식을 시스템에 전달하는 중간 객체
---

# AVAudioSession

> 원문 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession](https://developer.apple.com/documentation/avfoundation/avaudiosession)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class AVAudioSession : NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface AVAudioSession : NSObject
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 3.0+
> * UIKit for Mac 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## 개요

오디오 세션은 앱과 운영체제 \(또는 그 아래의 오디오 하드웨어\) 사이의 중간자 역할을 수행합니다. 오디오 세션을 사용하면 앱이 사용하는 오디오의 특성에 대해서 운영체제에 알림으로써 특정 오디오 동작이나 요구되는 하드웨어와의 상호작용을 자세히 설명할 필요가 없어집니다. 이 방식은 이런 오디오 세션의 세부사항 관리를 위임시켜서 운영체제가 사용자의 오디오 경험을 최상으로 관리하도록 합니다.

모든 iOS 및 tvOS 앱에는 다음과 같이 사전 설정된 기본 오디오 세션이 있습니다:

* 오디오 플레이백은 가능하지만 오디오 녹음은 허용되지 않습니다. \(tvOS에서는 오디오 녹음이 지원되지 않습니다.\)
* iOS에서는 스위치를 통해서 무음모드로 설정하면 앱에서 재생되는 모든 오디오가 음소거됩니다.
* iOS에서는 기기 화면이 꺼지면 \(잠겼을 때\) 앱 오디오가 음소거됩니다.
* 앱이 오디오를 재생할 때 다른 백그라운드 오디오들은 음소거됩니다.

기본 오디오 세션으로도 쓸만한 동작방식을 제공하기는 하지만 미디어 재 앱을 제작하기에는 충분하지 않을 수 있습니다. 기본 동작방식을 바꾸기 위해서는 오디오 세션의 카테고리를 설정해야 합니다.

AVFoundation에는 총 일곱가지의 사용가능한 카테고리가 있지만 \([Audio Session Categories and Modes](https://developer.apple.com/library/archive/documentation/Audio/Conceptual/AudioSessionProgrammingGuide/AudioSessionCategoriesandModes/AudioSessionCategoriesandModes.html#//apple_ref/doc/uid/TP40007875-CH10)를 참조하세요\) 재생 앱에서 가장 많이 사용되는 것은 플레이백\(playback\)입니다. 이 카테고리는 오디오 재생이 해당 앱의 중심 기능임을 알려줍니다. 여러분의 앱 오디오가 \(iOS에서\) 무음모드로 스위치가 전환되었을 때에도 재생되길 원한다면 이 카테고리를 지정하시면 됩니다. playback 카테고리는 오디오, AirPlay, PIP\(Picture in Picture\) 백그라운드 모드를 사용중일 때에도 앱의 백그라운드 오디오를 재생할 수 있도록 해줍니다. 더 자세한 내용은 [Enabling Background Audio](../../../etc/not-found.md) 문서를 참조하세요.

앱의 오디오 세션을 설정하기 위해서는 AVAudioSession이 사용됩니다. AVAudioSession은 싱글톤 객체로써 오디오 세션 카테고리 및 다른 설정을 수행합니다. 오디오 세션은 앱 생애주기 전체에 걸쳐서 상호작용할 수 있지만 보통은 다음 예시와 같이 앱이 최초 실행될 때 설정됩니다. 

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey : Any]?) -> Bool {
    let audioSession = AVAudioSession.sharedInstance()
    do {
        try audioSession.setCategory(AVAudioSessionCategoryPlayback)
    } catch {
        print("Setting category to AVAudioSessionCategoryPlayback failed.")
    }
    // Other project setup
    return true
}
```

이 카테고리는 setActive\(\_:\) 또는 setActive\(\_:options:\) 메서드를 사용하여 오디오 세션을 활성화 시켰을 때 사용됩니다.

{% hint style="info" %}
Note

카테고리를 설정한 후 언제든지 오디오 세션을 활성화 할 수 있지만 일반적으로는 앱에서 오디오 재생을 시작할 때까지 호출을 연기하는 것이 좋습니다. 호출을 연기함으로써 진행중인 다른 백그라운드 오디오가 너무 일찍 도중에 중단되지 않도록 할 수 있습니다.
{% endhint %}

## 주제

### First Steps

카테고리, 모드 및 선호 장치 세팅을 설정하려면 앱의 싱글톤 오디오 세션 인스턴스에 접근하세요.

* _class_ _func_ sharedInstance\(\) -&gt; AVAudioSession 공유 오디오 세션 인스턴스를 반환합니다.

### 오디오 세션 설정

오디오 세션의 카테고리, 모드, 옵션을 설정하세요.

* _var_ category: AVAudioSession.Category 현재 오디오 세션 카테고리
* _func_ setCategory\(AVAudioSession.Category\) 현재 오디오 세션 카테고리를 새로 설정합니다.
* _func_ setCategory\(AVAudioSession.Category, options: AVAudioSession.CategoryOptions\) 오디오 세션 카테고리를 지정된 옵션과 같이 설정합니다.
* _func_ setCategory\(AVAudioSession.Category, mode: AVAudioSession.Mode, options: AVAudioSession.CategoryOptions\) 오디오 세션을 지정된 카테고리, 모드, 옵션으로 설정합니다.
* _var_ availableCategories: \[AVAudioSession.Category\] 현재 기기에서 사용가능한 오디오 세션 카테고리
* _var_ categoryOptions: AVAudioSession.CategoryOptions 현재 오디오 세션 카테고리와 관련된 옵션 마스크
* _var_ mode: AVAudioSession.Mode 현재 오디오 세션 모드
* _func_ setMode\(AVAudioSession.Mode\)

  현재 오디오 세션 모드를 새로 설정합니다.

* _var_ availableModes: \[AVAudioSession.Mode\] 현재 기기에서 사용가능한 오디오 세션 모드

### 오디오 세션 활성화

설정된 카테고리와 옵션대로 오디오 세션을 활성화 합니다.

* _func_ setActive\(Bool, options: AVAudioSession.SetActiveOptions\) 지정된 옵션을 사용하여 앱의 오디오 세션을 활성화 또는 비활성화합니다.
* _func_ activate\(options: AVAudioSessionActivationOptions, completionHandler: \(Bool, Error?\) -&gt; Void\)

  watchOS의 오디오 세션을 비동기적으로 활성화합니다.

### 녹음 권한 요청

오디오 녹음을 위한 권한을 사용자에게 명시적으로 요청하세요.

오디오 녹음을 위해서는 사용자로부터 얻은 명시적인 허가가 필요합니다. 오디오 세션이 녹음이 가능한 카테고리를 통해 오디오의 입력 경로를 사용하려고 할 때 시스템은 자동적으로 사용자에게 사용 권한을 요구합니다. 그보다 일찍, 직접 사용 권한을 요구하고자 한다면 requestRecordPermission\(\_:\) 메서드를 사용할 수 있습니다. 사용자가 앱에 녹음 권한을 주기 전까지는 앱에서 녹음하더라도 아무것도 들을 수 없습니다.

* _var_ recordPermission: AVAudioSession.RecordPermission 현재 녹음 권한 상태값
* _func_ requestRecordPermission\(PermissionBlock\) 사용자에게 오디오 녹음 권한을 요청합니다.

### 다른 오디오에 응답

오디오 재생 방법, 또는 재생 여부를 결정하기 위해서 다른 앱에서 재생하고 있는 백그라운드 오디오가 있는지 확인하세요.

* _var_ isOtherAudioPlaying: Bool 다른 앱이 현재 오디오 재생중인지를 나타내는 Boolean 값
* _var_ secondaryAudioShouldBeSilencedHint: Bool

  A Boolean value that indicates whether another application is playing audio.

### 오디오 세션 노티피케이션에 응답

오디오 세션을 활성화 시키기 전에 상태 변화 노티피케이션의 수신을 등록하세요.

AVAudioSession은 세션 중단, 경로 변경, 미디어 서비스 리셋과 같은 중요한 상태 변화를 나타내는 노티피케이션을 발송합니다. 오디오 세션을 활성화 하기 전에 이런 노티피케이션의 수신을 등록하세요.

* 오디오 세션 인터럽트에 반응하기

  앱이 세션 인터럽트\(중단\)에 반응할 수 있도록 오디오 세션 노티피케이션을 직접 관찰\(observe\)합니다.

* 오디오 세션 경로 변경에 반응하기 앱이 세션 인터럽트\(중단\)에 반응할 수 있도록 오디오 세션 노티피케이션을 직접 관찰\(observe\)합니다.
* _class_ _let_ interruptionNotification: NSNotification.Name 오디오 중단이 발생한 경우 발송됩니다.
* _class_ _let_ routeChangeNotification: NSNotification.Name 시스템의 오디오 라우트 변경이 발생한 경우 발송됩니다.
* _class_ _let_ silenceSecondaryAudioHintNotification: NSNotification.Name 다른 응용프로그램의 기본 오디오가 시작되거나 중지될 경우 발송됩니다.
* _class_ _let_ mediaServicesWereLostNotification: NSNotification.Name 미디어 서버가 중단된 경우 발송됩니다.
* _class_ _let_ mediaServicesWereResetNotification: NSNotification.Name 미디어 서버가 재시작되었을 경우 발송됩니다.

### 오디오 경로 작업

오디오 경로\(route\)는 오디오 신호의 전기적인 통로입니다. 기기의 오디오 경로 상태를 점검하고 우선하는 입력/출력 경로를 설정하세요.

* _var_ currentRoute: AVAudioSessionRouteDescription 현재 오디오 입출력 경로를 설명하는 객체
* _var_ isInputAvailable: Bool 오디오 입력 경로의 사용가능 여부를 나타내는 Boolean 값
* _var_ availableInputs: \[AVAudioSessionPortDescription\]? 라우팅에 사용수 있는 입력 포트의 배열
* _var_ preferredInput: AVAudioSessionPortDescription? 우선되는 오디오 라우팅 입력 포트
* _func_ setPreferredInput\(AVAudioSessionPortDescription?\) 우선되는 오디오 라우팅 입력 포트를 설정합니다.
* _var_ inputDataSources: \[AVAudioSessionDataSourceDescription\]?

  현재 오디오 세션 입력 포트로 사용가능한 데이터 소스의 배열

* _var_ inputDataSource: AVAudioSessionDataSourceDescription? 현재 선택된 입력 데이터 소스
* _func_ setInputDataSource\(AVAudioSessionDataSourceDescription?\) 데이터 소스를 오디오 세션의 입력 포트로 선택합니다.
* _var_ outputDataSources: \[AVAudioSessionDataSourceDescription\]? 현재 오디오 출력 경로로 사용 가능한 데이터 소스의 배열
* _var_ outputDataSource: AVAudioSessionDataSourceDescription?

  현재 선택된 출력 데이터 소스

* _func_ setOutputDataSource\(AVAudioSessionDataSourceDescription?\) 오디오 세션의 출력 데이터 소스를 설정합니다.
* _func_ overrideOutputAudioPort\(AVAudioSession.PortOverride\)

  일시적으로 현재 오디오 경로를 변경합니다.

* _var_ routeSharingPolicy: AVAudioSession.RouteSharingPolicy

  현재 라우팅 정책

* _func_ setCategory\(AVAudioSession.Category, mode: AVAudioSession.Mode, policy: AVAudioSession.RouteSharingPolicy, options: AVAudioSession.CategoryOptions\)

  지정된 카테고리, 모드, 라우트 공유 정책과 옵션으로 세션을 설정합니다.

### 오디오 채널 작업

현재 오디오 장치에서 사용가능한 오디오 입출력 채널의 갯수를 점검하고 설정합니다.

* _var_ inputNumberOfChannels: Int

  현재 경로의 오디오 입력 채널 갯수

* _var_ maximumInputNumberOfChannels: Int

  현재 오디오 경로에서 사용가능한 최대 입력 채널 갯수

* _var_ preferredInputNumberOfChannels: Int 현재 경로의 기본 입력 채널 갯수
* _func_ setPreferredInputNumberOfChannels\(Int\) 현재 라우트의 기본 입력 채널 갯수를 설정합니다.
* _var_ outputNumberOfChannels: Int

  오디오 출력 채널 갯수

* _var_ maximumOutputNumberOfChannels: Int

  현재 오디오 경로에서 사용가능한 최대 출력 채널 갯수

* _var_ preferredOutputNumberOfChannels: Int 현재 경로의 기본 출력 채널 갯수
* _func_ setPreferredOutputNumberOfChannels\(Int\)

  현재 경로의 기본 출력 채널 갯수를 설정합니다.

### 오디오 장치 설정 작업

입력 게인, Sample rate, 입출력 버퍼 지속시간과 같은 오디오 장치 세팅을 검사하고 설정하세요.

* _var_ inputGain: Float

  세션과 관련된 입력에 적용되는 게인

* _var_ isInputGainSettable: Bool

  입력 게인이 설정 가능한지를 나타내는 Boolean 값

* _func_ setInputGain\(Float\) 입력 게인을 지정된 값으로 변경합니다.
* _var_ outputVolume: Float 사용자가 설정한 시스템 출력 볼륨
* _var_ inputLatency: TimeInterval

  초 단위로 측정되는 오디오 입력 지연시간

* _var_ outputLatency: TimeInterval 초 단위로 측정되는 오디오 출력 지연시간
* _var_ sampleRate: Double 헤르츠로 표시되는 현재 오디오 sample rate
* _var_ preferredSampleRate: Double 헤르츠로 표시되는 기본 sample rate
* _func_ setPreferredSampleRate\(Double\) 입출력의 기본 sample rate를 설정합니다.
* _var_ ioBufferDuration: TimeInterval 초 단위로 나타낸 현재 입출력 버퍼 지속시간
* _var_ preferredIOBufferDuration: TimeInterval 초 단위로 나타낸 기본 입출력 버퍼 지속시간
* _func_ setPreferredIOBufferDuration\(TimeInterval\) 기본 입출력 버퍼 지속시간을 초 단위로 설정합니다.

### Setting the Aggregated I/O Preference

Configure your preferred audio input behavior by setting your aggregated I/O preference.

Starting with iOS 10, [AVCaptureSession](../../../etc/not-found.md) has changed its default audio input configuration on iPhones and iPads that support the Live Photos feature. This change allows taking a Live Photo without interrupting background audio playback. Configure your preferred audio input behavior by setting your aggregated I/O preference.

* _func_ setAggregatedIOPreference\(AVAudioSession.IOType\)

  Sets the audio session's aggregated I/O configuration preference.

### 상수

* 오디오 세션 카테고리

  세션의 카테고리 속성을 설정하는데 사용되는 오디오 세션의 카테고리 식별자

* Audio Session Modes

  세션의 모드 속성을 설정하는데 사용되는 오디오 세션의 모드 식별자

* Audio Session Error Codes

  AVAudioSession 메서드에서 반환되는 NSError 객체에서 사용되는 에러 코드

* _enum_ AVAudioSession.RouteSharingPolicy 오디오 세션에 가능한 라우트 공유 정책을 나타내는 열거값

### 지원 타입

* _class_ AVAudioSessionChannelDescription 현재 장치의 하드웨어 채널에 대한 설명 정보를 제공합니다.
* _class_ AVAudioSessionDataSourceDescription 오디오 입출력 데이터 소스를 정의하고 소스의 이름과 위치, 방향 등의 정보를 제공합니다.
* _class_ AVAudioSessionPortDescription 포트의 기능과 포트에서 지원하는 하드웨어 채널에 대한 정보
* _class_ AVAudioSessionRouteDescription 세션의 현재 오디오 경로와 관련된 입출력 포트를 관리합니다.

### Type Aliases

* \_\_[_struct_ AVAudioSession.Category](../avfoundation/avaudiosession.category/)
* _struct_ AVAudioSession.Location
* \_\_[_struct_ AVAudioSession.Mode](../avfoundation/avaudiosession.mode.md)
* _struct_ AVAudioSession.Orientation
* _struct_ AVAudioSession.PolarPattern
* _struct_ AVAudioSession.Port

### 인스턴스 속성

* _var_ allowHapticsAndSystemSoundsDuringRecording: Bool `Beta`
* _var_ promptStyle: AVAudioSession.PromptStyle `Beta`

### 인스턴스 메서드

* _func_ prepareRouteSelectionForPlayback\(completionHandler: \(Bool, AVAudioSession.RouteSelection\) -&gt; Void\) `Beta`
* _func_ setAllowHapticsAndSystemSoundsDuringRecording\(Bool\) `Beta`

### 열거값

* _enum_ AVAudioSession.RouteSelection `Beta`
* _enum_ AVAudioSession.PromptStyle

## 관련 문서

### 상속

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

