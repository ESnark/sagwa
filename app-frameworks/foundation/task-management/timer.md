---
description: 특정 시간 간격이 경과한 후 호출되어 지정된 메세지를 target 객체에 보낸다.
---

# Timer

> 원문 출처  
> [https://developer.apple.com/documentation/foundation/timer](https://developer.apple.com/documentation/foundation/timer)

## Declaration

{% tabs %}
{% tab title="Swift" %}
```swift
class Timer: NSObject
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
@interface NSTimer : NSObject
```
{% endtab %}
{% endtabs %}

## Summary

> **SDKs**
>
> * iOS 2.0+
> * macOS 10.0+
> * Mac Catalyst 13.0+ `Beta`
> * tvOS 9.0+
> * watchOS 2.0+
>
> **Framework**
>
> * Foundation

## 개요 <a id="overview"></a>

Timer는 런 루프\(Run loop\)와 결합되어 동작합니다. 런 루프는 타이머에 대해 강한strong 참조를 유지하며 따라서 개발자는 런 루프에 추가된 타이머에 대해 직접 강한strong 참조를 유지할 필요가 없습니다.

Timer를 효과적으로 사용하기 위해서는 런 루프의 동작 방식에 대해 알 필요가 있습니다. 더 자세한 내용은 [Threading 프로그래밍 가이드](../../../documentation-archive/threading-programming-guide/)를 참조하세요.

Timer는 실시간 매커니즘이 아닙니다. 런 루프가 장시간 callout 중이거나 타이머를 감시하지 않는 모드에 들어가 있을 때 Timer의 실행 시간이 된다고 하더라도 런 루프가 다시 타이머를 감시하기 전까지 타이머는 실행되지 않습니다. 그러므로 실제 타이머가 실행되는 시간은 그보다 훨씬 나중이 될 것입니다. [Timer Tolerance](timer.md#time-tolerance)를 읽어보세요.

Timer는 toll-free Bridge로 Core Foundation의 CFRunLoopTimer와 상호 호환 가능합니다. [Toll-Free Brideging](../../../etc/not-found.md)에 대해서는 해당 문서를 참고하세요.

### 반복 타이머와 일회성 타이머의 비교 <a id="comparing-repeating-and-nonrepeating-timers"></a>

Timer는 생성시에 반복성인지 일회성인지를 지정하게 됩니다. 일회성 타이머는 한번 실행된 후 자동적으로 자기 자신을 무효화invalidate 시킴으로써 다시 실행되는 것을 방지합니다. 반면에 반복성 타이머는 실행 후 같은 런 루프에 자기 자신을 다시 스케줄링합니다. 반복성 타이머는 실제 실행시간이 아니라 예정된 시간에 따라 실행 시간을 스케줄링하게 됩니다. 예를 들어 타이머가 특정 시간에 실행된 이후 5초마다 반복적으로 실행되도록 예약된 경우 실제 실행 시간이 지연되더라도 예약되는 시간은 5초 간격으로 떨어집니다. 만약 실행 시간이 너무 많이 지연되어서 예약된 실행 시간을 하나 이상 지나쳤다면 타이머는 한번만 실행되고 다음의 실행을 위해 다시 예약을 잡습니다.

### Time Tolerance

iOS 7, macOS 10.9 부터는 타이머에 허용 오차를 지정할 수 있습니다. 타이머 실행시 제공되는 이 유연성은 시스템의 전력 효율과 응답성을 최적화하는데 도움을 줍니다. 타이머는 본래 스케줄링된 시간으로부터 허용 오차 시간동안 실행될 수 있습니다만 예약 시간보다 먼저 실행되지는 않습니다. 반복성 타이머에 적용된 경우, 다음 실행 시간은 허용 오차에 관계없이 원래 실행시간에 따라 계산됩니다. 이는 타이머가 밀리는 것을 방지하기 위함입니다. 기본값은 0이며 오차를 허용하지 않도록 설정되어 있음을 뜻합니다. 시스템은 지정된 [tolerance](../../../etc/not-found.md) 프로퍼티값과 별도로 약간의 허용 오차를 적용할 수 있는 권한을 가지고 있습니다.

타이머의 사용자로써 개발자는 타이머에 적절한 허용 오차를 결정할 수 있습니다. 반복성 타이머에 적용되는 일반적인 룰은 실행간격 시간의 10% 이상입니다. 적은 양의 허용 오차라도 앱 전력 소모량에 아주 긍정적인 효과를 가져옵니다. 시스템은 해당 허용 오차를 최대로 활용할 수 있습니다.

### 런 루프에 타이머 예약하기 <a id="scheduling-timers-in-run-loops"></a>

타이머를 동일한 런 루프의 여러 모드에 등록할 수는 있지만 여러개의 런 루프에 등록할 수는 없습니다. 타이머를 생성하는 방법에는 세가지가 있습니다:

* [scheduledTimer\(timeInterval:invocation:repeats:\)](../../../etc/not-found.md) 또는 [scheduledTimer\(timeInterval:target:selector:userInfo:repeats:\)](../../../etc/not-found.md) 클래스 메서드를 사용해서 타이머를 생성하고 현재 런 루프의 기본모드에 예약합니다.
* [init\(timeInterval:invocation:repeats:\)](../../../etc/not-found.md) 또는 [init\(timeInterval:target:selector:userInfo:repeats:\)](../../../etc/not-found.md) 클래스 메서드를 사용해서 런 루프에 예약하지 않고 타이머 객체만 생성합니다. \(생성한 후에는 등록할 RunLoop 객체의 [add\(\_:forMode:\)](../../../etc/not-found.md) 메서드를 호출해서 직접 타이머를 추가해야 합니다.\)
* [init\(fireAt:interval:target:selector:userInfo:repeats:\)](../../../etc/not-found.md) 메서드를 사용해서 타이머를 할당하고 초기화합니다. \(생성한 후에는 등록할 RunLoop 객체의 [add\(\_:forMode:\)](../../../etc/not-found.md) 메서드를 호출해서 직접 타이머를 추가해야 합니다.\)

한번 런 루프에 등록되면 타이머는 무효화될 때까지 지정된 시간 간격마다 실행됩니다. 일회성 타이머는 한번 실행되고 스스로를 무효화합니다. 하지만 반복성 타이머는 해당 객체의 [invalidate\(\)](../../../etc/not-found.md) 메서드를 실행해서 반드시 무효화되어야 합니다. 이 메서드를 호출하면 현재 런 루프에서 해당 타이머를 제거할 것을 요청하게 됩니다. 결과적으로 [invalidate\(\)](../../../etc/not-found.md) 메서드는 해당 타이머가 설치된 스레드에서 호출되어야만 합니다. 무효화된 타이머는 즉시 활성화되고 더이상 해당 런 루프에 영향을 줄 수 없습니다. 그리고 나서 런 루프는 [invalidate\(\)](../../../etc/not-found.md) 메서드가 리턴되기 전이나 그 후에 타이머 \(및 타이머에 대한 강한 참조\)를 제거합니다. 한번 무효화된 타이머 객체는 재사용될 수 없습니다.

### Subclassing Notes

[Timer](timer.md)는 서브클래싱하지 마세요.

## 주제

### Timer 생성

* _class func_ scheduledTimer\(withTimeInterval: TimeInterval, repeats: Bool, block: \(Timer\) -&gt; Void\) -&gt; Timer 타이머를 생성하고 현재 런 루프의 기본모드에 등록시킵니다.
* _class func_ scheduledTimer\(timeInterval: TimeInterval, target: Any, selector: Selector, userInfo: Any?, repeats: Bool\) -&gt; Timer 타이머를 생성하고 현재 런 루프의 기본모드에 등록시킵니다.
* _class func_ scheduledTimer\(timeInterval: TimeInterval, invocation: NSInvocation, repeats: Bool\) -&gt; Timer 타이머를 생성하고 현재 런 루프의 기본모드에 등록시킵니다.
* init\(timeInterval: TimeInterval, repeats: Bool, block: \(Timer\) -&gt; Void\)

  지정된 시간 간격과 block으로 타이머 객체를 초기화합니다.  
  Initializes a timer object with the specified time interval and block.

* init\(timeInterval: TimeInterval, target: Any, selector: Selector, userInfo: Any?, repeats: Bool\)  
  지정된 시간 간격과 selector로 타이머 객체를 초기화합니다.

  Initializes a timer object with the specified object and selector.

* init\(timeInterval: TimeInterval, invocation: NSInvocation, repeats: Bool\) 지정된 invocation 객체로 타이머 객체를 초기화합니다.
* init\(fire: Date, interval: TimeInterval, repeats: Bool, block: \(Timer\) -&gt; Void\) 지정된 날짜, 시간 간격과 block으로 타이머 객체를 초기화합니다.
* init\(fireAt: Date, interval: TimeInterval, target: Any, selector: Selector, userInfo: Any?, repeats: Bool\)

  지정된 객체와 selector로 타이머를 초기화합니다.

### Timer 실행

* _func_ fire\(\) timer의 메세지가 타겟에게 보내지도록 합니다.

### Timer 정지

* _func_ invalidate\(\) timer가 다시는 실행되지 않도록 하고 해당 런 루프로부터 제거되도록 요청합니다.

### Timer 정보 불러오기

* _var_ isValid: Bool

  timer가 현재 유효한지를 나타내는 Boolean 값

* _var_ fireDate: Date timer가 실행될 날짜
* _var_ timeInterval: TimeInterval 초 단위로 나타낸 timer의 시간 간격
* _var_ userInfo: Any? 수신자의 userInfo 객체

### 허용 오차 설정

* _var_ tolerance: TimeInterval 예약된 날짜 이후로 실행 가능한 시간범위

### Combine Publisher로써 메세지 발행하기

* _static func_ publish\(every: TimeInterval, tolerance: TimeInterval?, on: RunLoop, in: RunLoop.Mode, options: RunLoop.SchedulerOptions?\) -&gt; Timer.TimerPublisher

  지정된 시간간격에 따라 현재 date를 반복적으로 내보는 publisher를 반환합니다.

* _class_ Timer.TimerPublisher 지정된 시간간격에 따라 현재 date를 반복적으로 내보는 publisher

## 관련 문서

### 상속받은 대상

* NSObject

### 준수하는 프로토콜

* CVarArg
* Equatable
* Hashable

