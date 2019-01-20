# multiRoute

> 원문 출처  
> [https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616484-multiroute](https://developer.apple.com/documentation/avfoundation/avaudiosession/category/1616484-multiroute)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
static let multiRoute: AVAudioSession.Category
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
const AVAudioSessionCategory AVAudioSessionCategoryMultiRoute;
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 6.0+
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * AVFoundation

## Discussion

이 category는 입력, 출력 또는 둘 다 사용할 수 있습니다. 예를 들어 오디오를 USB 디바이스와 헤드셋 양쪽으로 라우트 하는데 이 category를 사용할 수 있습니다. 이 category를 사용할 때에는 사용가능한 오디오 라우트 기에 대해서 더 상세한 지식과 상호작용이 필요합니다.

{% hint style="warning" %}
Important

라우트 변경은 멀티 라우트 구성의 일부를 무효화할 수 있습니다. 이 Category를 사용할 때에는 [routeChangeNotification](../../../../etc/not-found.md)을 관찰하도록 등록시키고 필요에 따라서 구성을 업데이트 하는 것이 필수적입니다.
{% endhint %}

